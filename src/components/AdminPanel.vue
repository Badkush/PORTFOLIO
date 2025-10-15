<template>
  <div class="admin-panel" v-if="isAdmin">
    <div class="panel-header">
      <h2>🛡️ Panneau d'Administration - Détection d'IA</h2>
      <div class="panel-controls">
        <button @click="refreshData" class="btn-refresh" :disabled="loading">
          {{ loading ? '🔄' : '↻' }} Actualiser
        </button>
        <button @click="exportReport" class="btn-export">
          📄 Exporter
        </button>
        <button @click="clearLogs" class="btn-clear" :disabled="loading">
          🗑️ Vider les logs
        </button>
      </div>
    </div>

    <!-- Statistiques générales -->
    <div class="stats-grid">
      <div class="stat-card critical">
        <div class="stat-icon">🚨</div>
        <div class="stat-info">
          <div class="stat-number">{{ stats.critical || 0 }}</div>
          <div class="stat-label">Alertes Critiques</div>
        </div>
      </div>
      
      <div class="stat-card high">
        <div class="stat-icon">⚠️</div>
        <div class="stat-info">
          <div class="stat-number">{{ stats.high || 0 }}</div>
          <div class="stat-label">Risque Élevé</div>
        </div>
      </div>
      
      <div class="stat-card medium">
        <div class="stat-icon">👀</div>
        <div class="stat-info">
          <div class="stat-number">{{ stats.medium || 0 }}</div>
          <div class="stat-label">Surveillance</div>
        </div>
      </div>
      
      <div class="stat-card total">
        <div class="stat-icon">📊</div>
        <div class="stat-info">
          <div class="stat-number">{{ stats.total || 0 }}</div>
          <div class="stat-label">Total Détections</div>
        </div>
      </div>
    </div>

    <!-- Graphiques et analyse -->
    <div class="charts-section">
      <div class="chart-container">
        <h3>Détections par Type</h3>
        <div class="chart-placeholder">
          <div 
            v-for="(count, type) in detectionsByType" 
            :key="type"
            class="bar-item"
          >
            <div class="bar-label">{{ formatType(type) }}</div>
            <div class="bar-bg">
              <div 
                class="bar-fill" 
                :style="{ width: getBarWidth(count) + '%' }"
              ></div>
            </div>
            <div class="bar-count">{{ count }}</div>
          </div>
        </div>
      </div>

      <div class="chart-container">
        <h3>Activité par Heure</h3>
        <div class="hourly-chart">
          <div 
            v-for="hour in 24" 
            :key="hour-1"
            class="hour-bar"
            :title="`${hour-1}h: ${hourlyData[hour-1] || 0} détections`"
          >
            <div 
              class="hour-fill"
              :style="{ 
                height: getHourHeight(hourlyData[hour-1] || 0) + '%' 
              }"
            ></div>
            <div class="hour-label">{{ hour-1 }}</div>
          </div>
        </div>
      </div>
    </div>

    <!-- Liste des détections récentes -->
    <div class="detections-list">
      <h3>🕒 Détections Récentes</h3>
      <div class="list-controls">
        <select v-model="filterRisk" @change="filterDetections">
          <option value="">Tous les niveaux</option>
          <option value="critical">Critique</option>
          <option value="high">Élevé</option>
          <option value="medium">Moyen</option>
          <option value="low">Faible</option>
        </select>
        
        <select v-model="filterType" @change="filterDetections">
          <option value="">Tous les types</option>
          <option v-for="type in uniqueTypes" :key="type" :value="type">
            {{ formatType(type) }}
          </option>
        </select>
      </div>

      <div class="detections-table">
        <div class="table-header">
          <div class="col-time">Heure</div>
          <div class="col-type">Type</div>
          <div class="col-risk">Risque</div>
          <div class="col-ip">IP</div>
          <div class="col-details">Détails</div>
          <div class="col-actions">Actions</div>
        </div>
        
        <div 
          v-for="(detection, index) in filteredDetections" 
          :key="index"
          class="table-row"
          :class="getRiskClass(detection.risk)"
        >
          <div class="col-time">
            {{ formatTime(detection.timestamp) }}
          </div>
          <div class="col-type">
            <span class="type-badge">{{ formatType(detection.type) }}</span>
          </div>
          <div class="col-risk">
            <span class="risk-badge" :class="getRiskClass(detection.risk)">
              {{ detection.risk?.toUpperCase() }}
            </span>
          </div>
          <div class="col-ip">
            <code>{{ detection.ip || 'N/A' }}</code>
          </div>
          <div class="col-details">
            <button 
              @click="showDetails(detection)" 
              class="btn-details"
            >
              👁️ Voir
            </button>
          </div>
          <div class="col-actions">
            <button 
              @click="blockIP(detection.ip)" 
              class="btn-block"
              :disabled="!detection.ip"
            >
              🚫
            </button>
            <button 
              @click="whitelistIP(detection.ip)" 
              class="btn-whitelist"
              :disabled="!detection.ip"
            >
              ✅
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal de détails -->
    <div v-if="selectedDetection" class="modal-overlay" @click="closeModal">
      <div class="modal-content" @click.stop>
        <div class="modal-header">
          <h3>Détails de la Détection</h3>
          <button @click="closeModal" class="modal-close">×</button>
        </div>
        <div class="modal-body">
          <pre>{{ JSON.stringify(selectedDetection, null, 2) }}</pre>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'

// État réactif
const isAdmin = ref(false)
const loading = ref(false)
const detections = ref([])
const stats = ref({})
const detectionsByType = ref({})
const hourlyData = ref({})
const selectedDetection = ref(null)
const filterRisk = ref('')
const filterType = ref('')

// Authentification admin simple (à remplacer par votre système)
const adminPassword = 'admin123' // À CHANGER en production !

// Computed
const uniqueTypes = computed(() => 
  [...new Set(detections.value.map(d => d.type))]
)

const filteredDetections = computed(() => {
  let filtered = detections.value
  
  if (filterRisk.value) {
    filtered = filtered.filter(d => d.risk === filterRisk.value)
  }
  
  if (filterType.value) {
    filtered = filtered.filter(d => d.type === filterType.value)
  }
  
  return filtered.slice(0, 50) // Limiter à 50 résultats
})

// Méthodes
const authenticateAdmin = () => {
  const password = prompt('Mot de passe administrateur:')
  if (password === adminPassword) {
    isAdmin.value = true
    loadData()
  } else {
    alert('Mot de passe incorrect')
  }
}

const loadData = async () => {
  loading.value = true
  
  try {
    // Charger les détections depuis le service local
    const localDetections = getLocalDetections()
    detections.value = localDetections
    
    // Calculer les statistiques
    calculateStats()
    
    // Essayer de charger depuis le serveur
    await loadServerData()
    
  } catch (error) {
    console.error('Erreur lors du chargement des données:', error)
  } finally {
    loading.value = false
  }
}

const getLocalDetections = () => {
  try {
    const stored = localStorage.getItem('ai_detections') || '[]'
    return JSON.parse(stored)
  } catch (error) {
    return []
  }
}

const loadServerData = async () => {
  try {
    const response = await fetch('/api/ai-detection/stats', {
      headers: {
        'X-Admin-Token': 'your-admin-token' // À configurer
      }
    })
    
    if (response.ok) {
      const serverStats = await response.json()
      // Fusionner avec les données locales
      stats.value = { ...stats.value, ...serverStats }
    }
  } catch (error) {
    // Serveur non disponible, utiliser les données locales
    console.log('Utilisation des données locales uniquement')
  }
}

const calculateStats = () => {
  const riskCounts = detections.value.reduce((acc, detection) => {
    acc[detection.risk] = (acc[detection.risk] || 0) + 1
    return acc
  }, {})
  
  const typeCounts = detections.value.reduce((acc, detection) => {
    acc[detection.type] = (acc[detection.type] || 0) + 1
    return acc
  }, {})
  
  const hourlyCounts = detections.value.reduce((acc, detection) => {
    const hour = new Date(detection.timestamp).getHours()
    acc[hour] = (acc[hour] || 0) + 1
    return acc
  }, {})
  
  stats.value = {
    total: detections.value.length,
    critical: riskCounts.critical || 0,
    high: riskCounts.high || 0,
    medium: riskCounts.medium || 0,
    low: riskCounts.low || 0
  }
  
  detectionsByType.value = typeCounts
  hourlyData.value = hourlyCounts
}

const refreshData = () => {
  loadData()
}

const exportReport = () => {
  const report = {
    timestamp: new Date().toISOString(),
    stats: stats.value,
    detections: detections.value,
    summary: {
      totalDetections: detections.value.length,
      criticalAlerts: stats.value.critical,
      mostCommonType: Object.keys(detectionsByType.value)[0],
      peakHour: Object.keys(hourlyData.value).reduce((a, b) => 
        hourlyData.value[a] > hourlyData.value[b] ? a : b
      )
    }
  }
  
  const dataStr = JSON.stringify(report, null, 2)
  const dataBlob = new Blob([dataStr], { type: 'application/json' })
  const url = URL.createObjectURL(dataBlob)
  
  const link = document.createElement('a')
  link.href = url
  link.download = `ai-detection-report-${new Date().toISOString().split('T')[0]}.json`
  link.click()
  
  URL.revokeObjectURL(url)
}

const clearLogs = () => {
  if (confirm('Êtes-vous sûr de vouloir effacer tous les logs ?')) {
    detections.value = []
    localStorage.removeItem('ai_detections')
    calculateStats()
  }
}

const showDetails = (detection) => {
  selectedDetection.value = detection
}

const closeModal = () => {
  selectedDetection.value = null
}

const blockIP = (ip) => {
  if (ip && confirm(`Bloquer l'IP ${ip} ?`)) {
    // Ici, vous implémenteriez la logique de blocage
    console.log(`IP bloquée: ${ip}`)
    alert(`IP ${ip} bloquée (simulation)`)
  }
}

const whitelistIP = (ip) => {
  if (ip && confirm(`Ajouter l'IP ${ip} à la whitelist ?`)) {
    // Ici, vous implémenteriez la logique de whitelist
    console.log(`IP whitelistée: ${ip}`)
    alert(`IP ${ip} ajoutée à la whitelist (simulation)`)
  }
}

const filterDetections = () => {
  // La logique de filtrage est gérée par le computed
}

// Utilitaires
const formatType = (type) => {
  const typeNames = {
    'suspicious_user_agent': 'User Agent Suspect',
    'rapid_clicking': 'Clics Rapides',
    'no_mouse_movement': 'Pas de Mouvement',
    'massive_copy': 'Copie Massive',
    'ai_api_request': 'Requête API IA',
    'honeypot_triggered': 'Piège Déclenché',
    'repeated_copying': 'Copie Répétée'
  }
  
  return typeNames[type] || type.replace(/_/g, ' ').replace(/\b\w/g, l => l.toUpperCase())
}

const formatTime = (timestamp) => {
  return new Date(timestamp).toLocaleString('fr-FR')
}

const getRiskClass = (risk) => {
  return `risk-${risk}`
}

const getBarWidth = (count) => {
  const max = Math.max(...Object.values(detectionsByType.value))
  return max > 0 ? (count / max) * 100 : 0
}

const getHourHeight = (count) => {
  const max = Math.max(...Object.values(hourlyData.value))
  return max > 0 ? (count / max) * 100 : 0
}

// Initialisation
onMounted(() => {
  // Vérifier si l'utilisateur est déjà authentifié
  const isAuthenticated = sessionStorage.getItem('admin_authenticated')
  if (isAuthenticated === 'true') {
    isAdmin.value = true
    loadData()
  } else {
    authenticateAdmin()
  }
})
</script>

<style scoped>
.admin-panel {
  max-width: 1400px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Roboto', sans-serif;
}

.panel-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 30px;
  padding-bottom: 20px;
  border-bottom: 2px solid #F20E0E;
}

.panel-header h2 {
  color: #F20E0E;
  margin: 0;
}

.panel-controls {
  display: flex;
  gap: 10px;
}

.btn-refresh,
.btn-export,
.btn-clear {
  padding: 8px 16px;
  border: 1px solid #F20E0E;
  background: white;
  color: #F20E0E;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-refresh:hover,
.btn-export:hover {
  background: #F20E0E;
  color: white;
}

.btn-clear:hover {
  background: #dc3545;
  border-color: #dc3545;
  color: white;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
  margin-bottom: 30px;
}

.stat-card {
  display: flex;
  align-items: center;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.stat-card.critical { border-left: 4px solid #dc3545; }
.stat-card.high { border-left: 4px solid #fd7e14; }
.stat-card.medium { border-left: 4px solid #ffc107; }
.stat-card.total { border-left: 4px solid #28a745; }

.stat-icon {
  font-size: 2rem;
  margin-right: 15px;
}

.stat-number {
  font-size: 2rem;
  font-weight: bold;
  color: #333;
}

.stat-label {
  font-size: 0.9rem;
  color: #666;
}

.charts-section {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 30px;
  margin-bottom: 30px;
}

.chart-container {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.chart-container h3 {
  color: #F20E0E;
  margin-bottom: 20px;
}

.bar-item {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
  gap: 10px;
}

.bar-label {
  min-width: 120px;
  font-size: 0.8rem;
}

.bar-bg {
  flex: 1;
  height: 20px;
  background: #f0f0f0;
  border-radius: 10px;
  overflow: hidden;
}

.bar-fill {
  height: 100%;
  background: linear-gradient(90deg, #F20E0E, #ff4757);
  transition: width 0.5s ease;
}

.bar-count {
  min-width: 30px;
  text-align: right;
  font-weight: bold;
  color: #F20E0E;
}

.hourly-chart {
  display: flex;
  align-items: end;
  gap: 2px;
  height: 100px;
}

.hour-bar {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100%;
}

.hour-fill {
  width: 100%;
  background: linear-gradient(to top, #F20E0E, #ff4757);
  border-radius: 2px 2px 0 0;
  min-height: 2px;
  transition: height 0.5s ease;
}

.hour-label {
  font-size: 0.7rem;
  margin-top: 5px;
  color: #666;
}

.detections-list {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.detections-list h3 {
  color: #F20E0E;
  margin-bottom: 20px;
}

.list-controls {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.list-controls select {
  padding: 8px 12px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.detections-table {
  overflow-x: auto;
}

.table-header,
.table-row {
  display: grid;
  grid-template-columns: 120px 150px 80px 120px 80px 80px;
  gap: 15px;
  padding: 10px 0;
  border-bottom: 1px solid #eee;
  align-items: center;
}

.table-header {
  font-weight: bold;
  background: #f8f9fa;
  padding: 15px 0;
}

.table-row.risk-critical {
  background: rgba(220, 53, 69, 0.05);
}

.table-row.risk-high {
  background: rgba(253, 126, 20, 0.05);
}

.type-badge,
.risk-badge {
  padding: 4px 8px;
  border-radius: 12px;
  font-size: 0.75rem;
  font-weight: bold;
}

.type-badge {
  background: #e9ecef;
  color: #495057;
}

.risk-badge.risk-critical {
  background: #dc3545;
  color: white;
}

.risk-badge.risk-high {
  background: #fd7e14;
  color: white;
}

.risk-badge.risk-medium {
  background: #ffc107;
  color: #000;
}

.btn-details,
.btn-block,
.btn-whitelist {
  padding: 4px 8px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.8rem;
  margin-right: 5px;
}

.btn-details {
  background: #17a2b8;
  color: white;
}

.btn-block {
  background: #dc3545;
  color: white;
}

.btn-whitelist {
  background: #28a745;
  color: white;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10000;
}

.modal-content {
  background: white;
  border-radius: 8px;
  max-width: 600px;
  max-height: 80vh;
  overflow: auto;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  border-bottom: 1px solid #eee;
}

.modal-close {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
}

.modal-body {
  padding: 20px;
}

.modal-body pre {
  background: #f8f9fa;
  padding: 15px;
  border-radius: 4px;
  overflow-x: auto;
  font-size: 0.8rem;
}

@media (max-width: 768px) {
  .charts-section {
    grid-template-columns: 1fr;
  }
  
  .panel-header {
    flex-direction: column;
    gap: 15px;
  }
  
  .stats-grid {
    grid-template-columns: 1fr;
  }
  
  .table-header,
  .table-row {
    grid-template-columns: 1fr;
    text-align: left;
  }
}
</style>