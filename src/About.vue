<template>
  <section id="about" class="about-section">
    <div class="container">
      <div class="about-header">
        <h2 class="section-title">À propos de moi</h2>
        <div class="title-underline"></div>
      </div>
      
      <div class="about-content">
        <!-- Section principale avec photo et introduction -->
        <div class="intro-section">
          <div class="profile-container">
            <div class="profile-image-wrapper">
              <img 
                src="/images/gallery/profile-photo.jpg" 
                alt="Maxime Cuche - Développeur Web et Mobile" 
                class="profile-img"
              />
              <div class="profile-overlay">
                <div class="profile-text">
                  <h3>Maxime Cuche</h3>
                  <p>Développeur Passionné</p>
                </div>
              </div>
            </div>
          </div>
          
          <div class="intro-text">
            <h3 class="intro-title">
              Développeur Web et Mobile Indépendant
            </h3>
            <p class="intro-description">
              Passionné par le développement depuis plus de 5 ans, je transforme vos idées en solutions digitales 
              innovantes et performantes. Mon expertise couvre l'ensemble du cycle de développement, 
              de la conception à la mise en production.
            </p>
            
            <div class="personal-quote">
              <blockquote>
                "Chaque ligne de code est une opportunité de créer quelque chose d'exceptionnel."
              </blockquote>
            </div>
          </div>
        </div>
        
        <!-- Section des valeurs et philosophie -->
        <div class="values-section">
          <h3 class="subsection-title">Ma philosophie de travail</h3>
          <div class="values-grid">
            <div class="value-card">
              <div class="value-icon">🎯</div>
              <h4>Précision</h4>
              <p>Chaque détail compte. Je m'attache à livrer un code propre, optimisé et maintenable.</p>
            </div>
            
            <div class="value-card">
              <div class="value-icon">🚀</div>
              <h4>Innovation</h4>
              <p>Toujours à l'affût des dernières technologies pour proposer des solutions modernes.</p>
            </div>
            
            <div class="value-card">
              <div class="value-icon">🤝</div>
              <h4>Collaboration</h4>
              <p>L'écoute et la communication sont essentielles pour mener à bien chaque projet.</p>
            </div>
            
            <div class="value-card">
              <div class="value-icon">⚡</div>
              <h4>Performance</h4>
              <p>Des applications rapides et optimisées pour offrir la meilleure expérience utilisateur.</p>
            </div>
          </div>
        </div>
        
        <!-- Section expertise détaillée -->
        <div class="expertise-section">
          <h3 class="subsection-title">Mon expertise technique</h3>
          <div class="expertise-content">
            <div class="expertise-category">
              <h4 class="category-title">
                <span class="category-icon">🌐</span>
                Développement Frontend
              </h4>
              <div class="tech-grid">
                <span class="tech-badge">Vue.js</span>
                <span class="tech-badge">React</span>
                <span class="tech-badge">JavaScript ES6+</span>
                <span class="tech-badge">TypeScript</span>
                <span class="tech-badge">HTML5/CSS3</span>
                <span class="tech-badge">Sass/SCSS</span>
                <span class="tech-badge">Tailwind CSS</span>
                <span class="tech-badge">Responsive Design</span>
              </div>
            </div>
            
            <div class="expertise-category">
              <h4 class="category-title">
                <span class="category-icon">⚙️</span>
                Développement Backend
              </h4>
              <div class="tech-grid">
                <span class="tech-badge">Node.js</span>
                <span class="tech-badge">Express.js</span>
                <span class="tech-badge">PHP</span>
                <span class="tech-badge">Laravel</span>
                <span class="tech-badge">API REST</span>
                <span class="tech-badge">GraphQL</span>
                <span class="tech-badge">MongoDB</span>
                <span class="tech-badge">MySQL</span>
              </div>
            </div>
            
            <div class="expertise-category">
              <h4 class="category-title">
                <span class="category-icon">📱</span>
                Développement Mobile
              </h4>
              <div class="tech-grid">
                <span class="tech-badge">React Native</span>
                <span class="tech-badge">Flutter</span>
                <span class="tech-badge">PWA</span>
                <span class="tech-badge">Ionic</span>
                <span class="tech-badge">App Store</span>
                <span class="tech-badge">Google Play</span>
              </div>
            </div>
            
            <div class="expertise-category">
              <h4 class="category-title">
                <span class="category-icon">🛠️</span>
                Outils & DevOps
              </h4>
              <div class="tech-grid">
                <span class="tech-badge">Git</span>
                <span class="tech-badge">Vite</span>
                <span class="tech-badge">Webpack</span>
                <span class="tech-badge">Docker</span>
                <span class="tech-badge">CI/CD</span>
                <span class="tech-badge">AWS</span>
                <span class="tech-badge">Vercel</span>
                <span class="tech-badge">Netlify</span>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Section statistiques -->
        <div class="stats-section">
          <div class="stats-grid">
            <div class="stat-item">
              <div class="stat-number" ref="yearsExp">5+</div>
              <div class="stat-label">Années d'expérience</div>
            </div>
            <div class="stat-item">
              <div class="stat-number" ref="projectsCompleted">50+</div>
              <div class="stat-label">Projets réalisés</div>
            </div>
            <div class="stat-item">
              <div class="stat-number" ref="techMastered">25+</div>
              <div class="stat-label">Technologies maîtrisées</div>
            </div>
            <div class="stat-item">
              <div class="stat-number" ref="clientsSatisfied">30+</div>
              <div class="stat-label">Clients satisfaits</div>
            </div>
          </div>
        </div>
        
        <!-- Section passion et motivation -->
        <div class="passion-section">
          <h3 class="subsection-title">Ce qui me motive</h3>
          <div class="passion-content">
            <div class="passion-text">
              <p>
                Ma passion pour le développement va bien au-delà du simple code. J'aime comprendre les besoins métier, 
                analyser les défis techniques et proposer des solutions qui font vraiment la différence.
              </p>
              <p>
                Chaque projet est une nouvelle aventure qui me permet d'apprendre, d'innover et de repousser les limites 
                du possible. J'ai à cœur de créer des applications qui ne sont pas seulement fonctionnelles, 
                mais qui offrent une expérience utilisateur mémorable.
              </p>
            </div>
            
            <div class="motivation-list">
              <div class="motivation-item">
                <span class="motivation-icon">💡</span>
                <span>Résoudre des problèmes complexes avec élégance</span>
              </div>
              <div class="motivation-item">
                <span class="motivation-icon">🎨</span>
                <span>Créer des interfaces intuitives et esthétiques</span>
              </div>
              <div class="motivation-item">
                <span class="motivation-icon">📈</span>
                <span>Optimiser les performances et l'expérience utilisateur</span>
              </div>
              <div class="motivation-item">
                <span class="motivation-icon">🌟</span>
                <span>Transformer les idées en réalités digitales</span>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Call to action -->
        <div class="cta-section">
          <h3>Prêt à donner vie à votre projet ?</h3>
          <p>Discutons de vos besoins et créons ensemble quelque chose d'extraordinaire.</p>
          <button class="cta-button" @click="scrollToContact">
            Parlons de votre projet
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted, ref } from 'vue'

// Refs pour les statistiques
const yearsExp = ref(null)
const projectsCompleted = ref(null)
const techMastered = ref(null)
const clientsSatisfied = ref(null)

// Animation des compteurs
const animateCounters = () => {
  const counters = [
    { element: yearsExp.value, target: 5, suffix: '+' },
    { element: projectsCompleted.value, target: 50, suffix: '+' },
    { element: techMastered.value, target: 25, suffix: '+' },
    { element: clientsSatisfied.value, target: 30, suffix: '+' }
  ]
  
  counters.forEach(({ element, target, suffix }) => {
    if (element) {
      let current = 0
      const increment = target / 50
      const timer = setInterval(() => {
        current += increment
        if (current >= target) {
          element.textContent = target + suffix
          clearInterval(timer)
        } else {
          element.textContent = Math.ceil(current) + suffix
        }
      }, 40)
    }
  })
}

// Observer pour détecter quand la section est visible
const observeSection = () => {
  const options = {
    threshold: 0.3,
    rootMargin: '0px 0px -100px 0px'
  }
  
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        animateCounters()
        observer.unobserve(entry.target)
      }
    })
  }, options)
  
  const statsSection = document.querySelector('.stats-section')
  if (statsSection) {
    observer.observe(statsSection)
  }
}

// Fonction pour faire défiler vers la section contact
const scrollToContact = () => {
  const contactSection = document.querySelector('#contact')
  if (contactSection) {
    contactSection.scrollIntoView({ behavior: 'smooth' })
  }
}

onMounted(() => {
  observeSection()
})
</script>

<style scoped>
.about-section {
  background: linear-gradient(135deg, #FFFEEF 0%, rgba(255, 254, 239, 0.8) 100%);
  padding: 80px 0;
  min-height: 100vh;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Header de section */
.about-header {
  text-align: center;
  margin-bottom: 60px;
}

.section-title {
  font-size: 3em;
  color: #F20E0E;
  margin-bottom: 20px;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 2px;
}

.title-underline {
  width: 80px;
  height: 4px;
  background: linear-gradient(90deg, #F20E0E 0%, #ff4444 100%);
  margin: 0 auto;
  border-radius: 2px;
}

/* Section introduction */
.intro-section {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 50px;
  margin-bottom: 80px;
  align-items: center;
}

.profile-container {
  display: flex;
  justify-content: center;
}

.profile-image-wrapper {
  position: relative;
  width: 300px;
  height: 300px;
  border-radius: 50%;
  overflow: hidden;
  box-shadow: 0 20px 60px rgba(242, 14, 14, 0.3);
  transition: transform 0.3s ease;
}

.profile-image-wrapper:hover {
  transform: scale(1.05);
}

.profile-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.profile-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(transparent, rgba(242, 14, 14, 0.9));
  color: white;
  padding: 20px;
  text-align: center;
  transform: translateY(100%);
  transition: transform 0.3s ease;
}

.profile-image-wrapper:hover .profile-overlay {
  transform: translateY(0);
}

.profile-text h3 {
  margin: 0 0 5px 0;
  font-size: 1.3em;
  font-weight: bold;
}

.profile-text p {
  margin: 0;
  font-size: 0.9em;
  opacity: 0.9;
}

.intro-title {
  color: #F20E0E;
  font-size: 2.2em;
  margin-bottom: 20px;
  font-weight: bold;
  line-height: 1.2;
}

.intro-description {
  font-size: 1.1em;
  line-height: 1.8;
  color: #333;
  margin-bottom: 30px;
  text-align: justify;
}

.personal-quote {
  background: rgba(242, 14, 14, 0.05);
  padding: 25px;
  border-left: 4px solid #F20E0E;
  border-radius: 8px;
}

.personal-quote blockquote {
  margin: 0;
  font-style: italic;
  font-size: 1.1em;
  color: #555;
  position: relative;
}

.personal-quote blockquote::before {
  content: '"';
  font-size: 3em;
  color: #F20E0E;
  position: absolute;
  top: -10px;
  left: -20px;
}

/* Section des valeurs */
.values-section {
  margin-bottom: 80px;
}

.subsection-title {
  font-size: 2em;
  color: #F20E0E;
  text-align: center;
  margin-bottom: 40px;
  font-weight: bold;
}

.values-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 30px;
}

.value-card {
  background: white;
  padding: 30px;
  border-radius: 15px;
  text-align: center;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.value-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 50px rgba(242, 14, 14, 0.2);
}

.value-icon {
  font-size: 3em;
  margin-bottom: 20px;
  display: block;
}

.value-card h4 {
  color: #F20E0E;
  font-size: 1.4em;
  margin-bottom: 15px;
  font-weight: bold;
}

.value-card p {
  color: #666;
  line-height: 1.6;
}

/* Section expertise */
.expertise-section {
  margin-bottom: 80px;
}

.expertise-content {
  display: grid;
  gap: 40px;
}

.expertise-category {
  background: white;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.category-title {
  display: flex;
  align-items: center;
  gap: 15px;
  color: #F20E0E;
  font-size: 1.4em;
  margin-bottom: 25px;
  font-weight: bold;
}

.category-icon {
  font-size: 1.5em;
}

.tech-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}

.tech-badge {
  background: linear-gradient(135deg, #F20E0E 0%, #ff4444 100%);
  color: white;
  padding: 8px 16px;
  border-radius: 20px;
  font-size: 0.9em;
  font-weight: 500;
  transition: transform 0.2s ease;
}

.tech-badge:hover {
  transform: scale(1.05);
}

/* Section statistiques */
.stats-section {
  margin-bottom: 80px;
  background: linear-gradient(135deg, #F20E0E 0%, #ff4444 100%);
  color: white;
  padding: 50px 30px;
  border-radius: 20px;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 30px;
  text-align: center;
}

.stat-item {
  padding: 20px;
}

.stat-number {
  font-size: 3.5em;
  font-weight: bold;
  margin-bottom: 10px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

.stat-label {
  font-size: 1.1em;
  opacity: 0.9;
  text-transform: uppercase;
  letter-spacing: 1px;
}

/* Section passion */
.passion-section {
  margin-bottom: 60px;
}

.passion-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 50px;
  align-items: start;
}

.passion-text p {
  font-size: 1.1em;
  line-height: 1.8;
  color: #333;
  margin-bottom: 20px;
  text-align: justify;
}

.motivation-list {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.motivation-item {
  display: flex;
  align-items: center;
  gap: 15px;
  background: white;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s ease;
}

.motivation-item:hover {
  transform: translateX(10px);
}

.motivation-icon {
  font-size: 1.8em;
  flex-shrink: 0;
}

/* Call to action */
.cta-section {
  text-align: center;
  background: white;
  padding: 50px;
  border-radius: 20px;
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.1);
}

.cta-section h3 {
  color: #F20E0E;
  font-size: 2em;
  margin-bottom: 15px;
  font-weight: bold;
}

.cta-section p {
  font-size: 1.2em;
  color: #666;
  margin-bottom: 30px;
}

.cta-button {
  background: linear-gradient(135deg, #F20E0E 0%, #ff4444 100%);
  color: white;
  border: none;
  padding: 15px 40px;
  font-size: 1.1em;
  font-weight: bold;
  border-radius: 30px;
  cursor: pointer;
  transition: all 0.3s ease;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.cta-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 25px rgba(242, 14, 14, 0.4);
}

/* Responsive Design */
@media (max-width: 768px) {
  .about-section {
    padding: 60px 0;
  }
  
  .section-title {
    font-size: 2.2em;
  }
  
  .intro-section {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 30px;
  }
  
  .profile-image-wrapper {
    width: 250px;
    height: 250px;
  }
  
  .intro-title {
    font-size: 1.8em;
  }
  
  .values-grid {
    grid-template-columns: 1fr;
  }
  
  .passion-content {
    grid-template-columns: 1fr;
    gap: 30px;
  }
  
  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 15px;
  }
  
  .section-title {
    font-size: 1.8em;
  }
  
  .profile-image-wrapper {
    width: 200px;
    height: 200px;
  }
  
  .intro-title {
    font-size: 1.5em;
  }
  
  .stats-grid {
    grid-template-columns: 1fr;
  }
  
  .stat-number {
    font-size: 2.5em;
  }
  
  .cta-section {
    padding: 30px 20px;
  }
}
</style>