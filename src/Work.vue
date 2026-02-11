<template>
    <section id="work" class="work">
        <div class="container">
            <h2 class="section-title">Mes Compétences & Outils</h2>
            
            <div class="skills-grid">
                <div 
                    v-for="skill in skills" 
                    :key="skill.id"
                    class="skill-card"
                    @mouseenter="playHoverAnimation"
                >
                    <div class="skill-icon">
                        <img :src="skill.icon" :alt="skill.name" />
                    </div>
                    <div class="skill-info">
                        <h3 class="skill-name">{{ skill.name }}</h3>
                        <div class="skill-level">
                            <div class="level-bar">
                                <div 
                                    class="level-fill" 
                                    :style="{ width: skill.level + '%' }"
                                ></div>
                            </div>
                            <span class="level-text">{{ skill.level }}%</span>
                        </div>
                        <p class="skill-description">{{ skill.description }}</p>
                    </div>
                </div>
            </div>

            <!-- Section Projets -->
            <div class="projects-section">
                <h3 class="projects-title">Projets Récents</h3>
                <div class="projects-grid">
                    <div 
                        v-for="project in projects" 
                        :key="project.id"
                        class="project-card"
                    >
                        <div class="project-image" @click="openImageInNewWindow(project)">
                            <img :src="project.image" :alt="project.title" />
                            <div class="project-overlay">
                                <span class="view-project">Voir l'image en grand</span>
                            </div>
                        </div>
                        <div class="project-content">
                            <h4 class="project-title">{{ project.title }}</h4>
                            <p class="project-description">{{ project.description }}</p>
                            <div class="project-technologies">
                                <span 
                                    v-for="tech in project.technologies" 
                                    :key="tech"
                                    class="tech-tag"
                                >
                                    {{ tech }}
                                </span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

// Données des compétences
const skills = ref([
  {
    id: 1,
    name: 'Figma',
    level: 90,
    description: 'Design UI/UX et prototypage',
    icon: "/PORTFOLIO/figma-official-logo.svg"
  },
  {
    id: 2,
    name: 'HTML5',
    level: 95,
    description: 'Structure et sémantique web',
    icon: '/PORTFOLIO/html5-logo.svg'
  },
  {
    id: 3,
    name: 'CSS3',
    level: 95,
    description: 'Styles et animations avancées',
    icon: '/PORTFOLIO/css3-official-logo.svg'
  },
  {
    id: 4,
    name: 'JavaScript',
    level: 90,
    description: 'Programmation dynamique',
    icon: '/PORTFOLIO/javascript-official-logo.svg'
  },
  { 
    id: 5,
    name: 'Vue.js',
    level: 90,
    description: 'Framework réactif moderne',
    icon: '/PORTFOLIO/vuejs-logo.svg'
  },
  {
    id: 6,
    name: 'Mobile Design',
    level: 50,
    description: 'Applications mobiles natives',
    icon: "/PORTFOLIO/mobile-design-official-logo.svg"
  }
])

// Données des projets
const projects = ref([
  {
    id: 1,
    title: 'Creation de fond d\'écran rétro',
    description: 'Design d\'un fond d\'écran rétro pour un client',
    image: './images/gallery/hawaii style retro commic.jpg',
    technologies: ['figma'],
    url: './images/gallery/hawaii style retro commic.jpg'
  },
  {
    id: 2,
    title: 'Site vitrine pour Udemy',
    description: 'Interface d\'administration avec graphiques interactifs',
    image: './images/gallery/site web.jpg',
    technologies: ['HTML5', 'CSS3', 'JavaScript'],
    url: './images/gallery/site web.jpg'
  },
  {
    id: 3,
    title: 'App Mobile Figma',
    description: 'Design d\'application mobile pour un coffee shop',
    image: './images/gallery/coffee shop.png',
    technologies: ['Figma', 'Design System', 'Prototyping'],
    url: './images/gallery/coffee shop.png'
  }
])

// Fonctions d'interaction 
const playHoverAnimation = (event) => {

  // Animation au survol
  const card = event.currentTarget
  card.style.transform = 'translateY(-5px)'

  // Revenir à la position initiale après l'animation
  setTimeout(() => {
    card.style.transform = ''
  }, 300)
}

// Fonction pour ouvrir l'image du projet dans une nouvelle fenêtre
const openImageInNewWindow = (project) => {
  if (project.image) {
    // Ouvre l'image dans une nouvelle fenêtre/onglet
    window.open(project.image, '_blank', 'width=800,height=600,scrollbars=yes,resizable=yes')
  } else {
    // Si aucune image n'est disponible, afficher une alerte  
    alert('Aucune image disponible pour ce projet.')
  }
}

// Animation au chargement
onMounted(() => {
  const cards = document.querySelectorAll('.skill-card')

  // La méthode forEach permet d'exécuter une fonction donnée sur chaque élément du tableau.
  cards.forEach((card, index) => {
    setTimeout(() => {
      card.style.opacity = '1'
      card.style.transform = 'translateY(0)' 
    }, index * 100)
  })
})
</script>

<style scoped>
.work {
  background: linear-gradient(135deg, #FFFEEF 0%, #f8f4e6 100%); /* Dégradé de fond pour un effet plus doux */                    
  padding: 80px 0;
  min-height: 100vh;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.section-title {
  text-align: center;
  font-size: 2.5rem;
  color: #F20E0E;
  margin-bottom: 60px;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 2px;
}

/* Grille des compétences */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr)); /* Ajuste le nombre de colonnes en fonction de la largeur disponible */
  gap: 30px;
  margin-bottom: 80px;
  cursor: pointer;
}

.skill-card {
  background: white;
  border-radius: 15px;
  padding: 25px;
  box-shadow: 0 10px 30px rgba(242, 14, 14, 0.1);
  transition: all 0.3s ease;
  opacity: 0;
  transform: translateY(30px); /* Position initiale pour l'animation d'entrée */
  border: 2px solid transparent;
}

.skill-card:hover {
  transform: translateY(-10px); /* Position finale pour l'animation au survol */
  box-shadow: 0 20px 40px rgba(242, 14, 14, 0.2);
  border-color: #F20E0E;
}

.skill-icon {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.skill-icon img {
  width: 60px;
  height: 60px;
  object-fit: contain; /* Assure que l'image garde ses proportions sans déformation */
  border-radius: 8px;
}

.skill-info {
  text-align: center;
  cursor: default;
}

.skill-name {
  font-size: 1.4rem;
  color: #F20E0E;
  margin-bottom: 15px;
  font-weight: bold;
}

.skill-level {
  display: flex;
  align-items: center;
  gap: 15px;
  margin-bottom: 15px;
}

.level-bar {
  flex: 1;
  height: 8px;
  background: #f0f0f0;
  border-radius: 10px;
  overflow: hidden; /* Assure que le remplissage ne dépasse pas les bords */
}

.level-fill {
  height: 100%;
  background: linear-gradient(90deg, #F20E0E, #ff4757);
  border-radius: 10px;
  transition: width 1s ease; /* Transition pour l'animation de la barre de niveau */
}

.level-text {
  font-weight: bold;
  color: #F20E0E;
  min-width: 40px;
}

.skill-description {
  color: #666;
  font-size: 0.95rem;
  line-height: 1.5;
}

/* Section Projets */
.projects-section {
  margin-top: 60px;
  cursor: pointer;
}

.projects-title {
  text-align: center;
  font-size: 2rem;
  color: #F20E0E;
  margin-bottom: 40px;
  font-weight: bold;
}

/* Grille des projets */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 30px;
}

/* Carte de projet */
.project-card {
  background: white;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

/* Effet de levitation au survol */
.project-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 15px 35px rgba(242, 14, 14, 0.15);
}

/* Image du projet avec effet de zoom au survol */
.project-image {
  position: relative;
  height: 200px;
  overflow: hidden;
  cursor: pointer;
}

/* Image du projet avec effet de zoom au survol */
.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover; /* Assure que l'image couvre toute la zone sans déformation */
  transition: transform 0.3s ease; /* Transition pour l'effet de zoom */
}

/* Overlay rouge avec texte centré */
.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(242, 14, 14, 0.9);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease; /* Transition pour l'apparition de l'overlay */
}

.project-card:hover .project-overlay {
  opacity: 1; /* Affiche l'overlay au survol de la carte */
}

.project-card:hover .project-image img {
  transform: scale(1.1); /* Effet de zoom au survol */
}

/* Texte du bouton "Voir l'image en grand" */
.view-project {
  color: white;
  font-weight: bold;
  font-size: 1.1rem;
  text-transform: uppercase;
  letter-spacing: 1px;
}

/* Contenu du projet */
.project-content {
  padding: 25px;
}

.project-title {
  font-size: 1.3rem;
  color: #F20E0E;
  margin-bottom: 10px;
  font-weight: bold;
}

.project-description {
  color: #666;
  line-height: 1.6;
  margin-bottom: 20px;
}

.project-technologies {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

/* Tag de technologies */
.tech-tag {
  background: #F20E0E;
  color: white;
  padding: 4px 12px;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 500;
}

/* Responsive Design */
@media (max-width: 768px) {
  .section-title {
    font-size: 2rem;
    margin-bottom: 40px;
  }
  
  .skills-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }
  
  .skill-card {
    padding: 20px;
  }
  
  .projects-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }
  
  .work {
    padding: 40px 0;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 15px;
  }
  
  .section-title {
    font-size: 1.6rem;
    letter-spacing: 1px;
  }
  
  .skill-level {
    flex-direction: column;
    gap: 8px;
  }
  
  .level-text {
    align-self: flex-end;
  }
}

/* Animation d'entrée */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>