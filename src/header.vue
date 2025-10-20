<template>

  <header style="padding-right: 80px; padding-left: 80px;">
    <nav class="navsection">     
        <div class="navigation" style="padding-top: 3em;">
            <!-- Section gauche : name et metier -->
            <div 
                class="logo-section"
                @click="scrollToTop"
                title="Retour au début de la page"
            >
                <div class="logo">
                    <p class="name">
                        maxime Cuche
                    <br>
                    <span class="metier">Développeur web et mobile indépendant</span>
                    </p>
                </div>
            </div>
            
            <!-- Section centre : Photo de profil -->
            <div class="profile-section">
                <div class="profile-image-container">
                    <img 
                        src="/images/gallery/profile-photo.jpg"
                        alt="Photo de profil de Maxime Cuche" 
                        class="profile-image"
                    />
                </div>
            </div>
            
            <!-- Section droite : Navigation -->
            <div class="nav-section">
                <div class="links">
                    <a href="#work" class="nav-link">work</a>
                    <a href="#" @click="openAboutModal" class="nav-link">about me</a>
                    <a href="#contact" class="nav-link">contact</a>
                    <a 
                        href="#"
                        @click="openOutlookEmail" 
                        @contextmenu="showEmailOptions"
                        class="email"
                        title="Clic gauche: Outlook | Clic droit: Options"
                    >
                        maxcuche46@gmail.com
                    </a>                    
                </div>
            </div>
        </div>      
    </nav>
  </header>

  <!-- Modal About Me -->
  <div v-if="showModal" class="modal-overlay" @click="closeModal">
    <div class="modal-content" @click.stop>
      <div class="modal-header">
        <h2>À propos de moi</h2>
        <button class="close-btn" @click="closeModal">&times;</button>
      </div>
      
      <div class="modal-body">
        <div class="about-content">
          <div class="about-image">
            <img src="/images/gallery/me.jpg" alt="Maxime Cuche" class="about-profile-img">
          </div>
          
          <div class="about-text">
            <h3>Maxime Cuche</h3>
            <p class="about-title">Développeur Web et Mobile Indépendant</p>
            
            <div class="about-description">
              <p>
                Passionné par le développement web et mobile depuis plus de 5 ans, je crée des applications 
                modernes et performantes qui répondent aux besoins de mes clients.
              </p>
              
              <p>
                Spécialisé dans les technologies JavaScript (Vue.js, React, Node.js), je maîtrise également 
                le développement mobile avec React Native et Flutter.
              </p>
              
              <div class="skills-grid">
                <div class="skill-category">
                  <h4>Frontend</h4>
                  <ul>
                    <li>Vue.js / React</li>
                    <li>HTML5 / CSS3</li>
                    <li>JavaScript ES6+</li>
                    <li>Responsive Design</li>
                  </ul>
                </div>
                
                <div class="skill-category">
                  <h4>Backend</h4>
                  <ul>
                    <li>Node.js / Express</li>
                    <li>PHP / Laravel</li>
                    <li>MongoDB / MySQL</li>
                    <li>API REST</li>
                  </ul>
                </div>
                
                <div class="skill-category">
                  <h4>Mobile</h4>
                  <ul>
                    <li>React Native</li>
                    <li>Flutter</li>
                    <li>Progressive Web Apps</li>
                    <li>App Store / Play Store</li>
                  </ul>
                </div>
              </div>
              
              <div class="contact-cta">
                <p>Vous avez un projet en tête ? Discutons-en !</p>
                <button class="cta-btn" @click="contactMe">Me contacter</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>

<script setup>
// Fonction pour ouvrir Outlook avec email prédéfini
const openOutlookEmail = (event) => {
  event.preventDefault()
  
  // Paramètres de l'email
  const emailData = {
    to: 'maxcuche46@gmail.com',
    subject: 'Contact depuis le site web - Maxime Cuche',
    body: `Bonjour Maxime,

Je vous contacte via votre site web concernant vos services de développement web et mobile.

Projet : [Décrivez votre projet]
Budget estimé : [Votre budget]
Délais souhaités : [Vos délais]

Cordialement,
[Votre nom]
[Votre entreprise]
[Votre téléphone]`
  }
  
  // Détecter le navigateur et l'OS pour choisir la meilleure méthode
  const isWindows = navigator.platform.toLowerCase().includes('win')
  const isMobile = /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)
  
  // Construction des URLs
  const outlookWebUrl = `https://outlook.live.com/mail/0/deeplink/compose?to=${encodeURIComponent(emailData.to)}&subject=${encodeURIComponent(emailData.subject)}&body=${encodeURIComponent(emailData.body)}`
  const outlookDesktopUrl = `ms-outlook://compose?to=${emailData.to}&subject=${encodeURIComponent(emailData.subject)}&body=${encodeURIComponent(emailData.body)}`
  const mailtoUrl = `mailto:${emailData.to}?subject=${encodeURIComponent(emailData.subject)}&body=${encodeURIComponent(emailData.body)}`
  
  // Stratégie d'ouverture selon le contexte
  if (isWindows && !isMobile) {
    // Sur Windows desktop : essayer Outlook desktop d'abord
    try {
      window.location.href = outlookDesktopUrl
      
      // Fallback vers Outlook Web après 2 secondes si l'app desktop ne s'ouvre pas
      setTimeout(() => {
        if (confirm('Outlook ne semble pas installé. Voulez-vous utiliser Outlook Web ?')) {
          window.open(outlookWebUrl, '_blank', 'width=900,height=700,scrollbars=yes,resizable=yes')
        } else {
          // Dernier recours : client email par défaut
          window.location.href = mailtoUrl
        }
      }, 2000)
      
    } catch (error) {
      // Si erreur, utiliser Outlook Web
      window.open(outlookWebUrl, '_blank', 'width=900,height=700,scrollbars=yes,resizable=yes')
    }
  } else {
    // Sur autres plateformes : Outlook Web ou mailto
    const outlookWindow = window.open(outlookWebUrl, '_blank', 'width=900,height=700,scrollbars=yes,resizable=yes')
    
    // Fallback si le popup est bloqué
    if (!outlookWindow) {
      alert('Popup bloqué. Redirection vers votre client email par défaut.')
      window.location.href = mailtoUrl
    }
  }
  
  // Optionnel : Analytics ou tracking
  console.log('Email contact initié vers:', emailData.to)
}

// Fonction pour remonter en haut de la page
const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  })
}

// Fonction pour gérer l'effet de scroll sur le header
import { onMounted, onUnmounted, ref } from 'vue'

let isScrolled = false

// Gestion du modal About Me
const showModal = ref(false)

const openAboutModal = (event) => {
  event.preventDefault()
  showModal.value = true
  // Empêcher le scroll du body quand le modal est ouvert
  document.body.style.overflow = 'hidden'
}

const closeModal = () => {
  showModal.value = false
  // Rétablir le scroll du body
  document.body.style.overflow = 'auto'
}

// Fonction pour contacter depuis le modal
const contactMe = () => {
  closeModal()
  // Faire défiler vers la section contact ou ouvrir l'email
  const contactSection = document.querySelector('#contact')
  if (contactSection) {
    contactSection.scrollIntoView({ behavior: 'smooth' })
  } else {
    // Ouvrir l'email si pas de section contact
    openOutlookEmail(new Event('click'))
  }
}

// Fermer le modal avec la touche Échap
const handleEscKey = (event) => {
  if (event.key === 'Escape' && showModal.value) {
    closeModal()
  }
}

const handleScroll = () => {
  const header = document.querySelector('header')
  if (window.scrollY > 50) {
    if (!isScrolled) {
      header.classList.add('scrolled')
      isScrolled = true
    }
  } else {
    if (isScrolled) {
      header.classList.remove('scrolled')
      isScrolled = false
    }
  }
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  window.addEventListener('keydown', handleEscKey)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  window.removeEventListener('keydown', handleEscKey)
})

// Fonction pour afficher les options au clic droit
const showEmailOptions = (event) => {
  event.preventDefault()
  
  const email = 'maxcuche46@gmail.com'
  
  const choice = confirm(`Options pour ${email}:
  
OK = Copier l'email dans le presse-papiers
Annuler = Ouvrir le client email par défaut`)
  
  if (choice) {
    // Copier dans le presse-papiers
    copyEmailToClipboard(email)
  } else {
    // Ouvrir avec client par défaut
    window.location.href = `mailto:${email}`
  }
}

// Fonction pour copier l'email dans le presse-papiers
const copyEmailToClipboard = async (email) => {
  try {
    await navigator.clipboard.writeText(email)
    
    // Animation de confirmation
    const emailElement = event.target
    const originalText = emailElement.textContent
    
    emailElement.textContent = '📋 Copié !'
    emailElement.style.color = '#28a745'
    
    setTimeout(() => {
      emailElement.textContent = originalText
      emailElement.style.color = ''
    }, 2000)
    
    console.log('Email copié:', email)
  } catch (err) {
    // Fallback pour navigateurs plus anciens
    const textArea = document.createElement('textarea')
    textArea.value = email
    document.body.appendChild(textArea)
    textArea.select()
    document.execCommand('copy')
    document.body.removeChild(textArea)
    
    alert(`Email copié: ${email}`)
  }
}
</script>

<style scoped>
header {
  background-color: #FFFEEF;
  color: #F20E0E;
  font-size: 20px;
  font-weight: bold;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  box-shadow: 0 2px 10px rgba(242, 14, 14, 0.1);
  backdrop-filter: blur(10px);
  transition: all 0.3s ease;
}

/* Effet au scroll */
header.scrolled {
  background-color: rgba(255, 254, 239, 0.95);
  box-shadow: 0 4px 20px rgba(242, 14, 14, 0.2);
  backdrop-filter: blur(15px);
}

header.scrolled .navigation {
  padding: 10px 20px;
}
.navigation {
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
  padding: 15px 20px;
}

/* Section gauche */
.logo-section {
  display: flex;
  justify-content: flex-start;
  cursor: pointer;
  transition: opacity 0.3s ease;
}

.logo-section:hover {
  opacity: 0.8;
}

/* Section centre */
.profile-section {
  position: absolute;   
  left: 50%;  
  transform: translateX(-50%);
  z-index: 10; /* Assure que l'image est au-dessus des autres sections */
}

.profile-image-container {
  display: flex;
  align-items: center;
  justify-content: center;
}

.profile-image {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  border: 3px solid #F20E0E;
  transition: all 0.3s ease;
  cursor: pointer;
  /* Ombre plus prononcée avec plusieurs couches */
  box-shadow: 
    0 8px 16px #F20E0E(242, 14, 14, 0.4),
    0 4px 8px #F20E0E(242, 14, 14, 0.3),
    0 2px 4px rgba(0, 0, 0, 0.2);
}

.profile-image:hover {
  transform: scale(1.1);
  /* Ombre plus intense au survol */
  box-shadow: 
    0 12px 24px rgba(242, 14, 14, 0.5), /* Ombre encore plus large */
    0 8px 16px rgba(242, 14, 14, 0.4),  /* Ombre moyenne */
    0 4px 8px rgba(0, 0, 0, 0.3);       /* Ombre de base renforcée */
}

/* Section droite */
.nav-section {
  flex: 1;
  display: flex;
  justify-content: flex-end;
}
.navsection {
  width: 100%; 
}
.logo {
  text-decoration: none;
  color: #F20E0E;
  letter-spacing: -0.10px;
  font-size: 1.2em;
}
.name {
  text-transform: uppercase;
  font-weight: bold;
  margin: 0;
  line-height: 1.2;
}
.metier {
  text-transform: capitalize;
  font-weight: normal;
  margin: 0;
}
a {
  color: #F20E0E;
  text-decoration: none;
}
.links {
  display: flex;  
  align-items: center;
  gap: 20px;
}
.email {
    font-weight: bold;
    text-decoration: solid underline;
    color: #F20E0E;
    position: relative;
    cursor: pointer;
    transition: all 0.3s ease;
    padding: 8px 12px;
    border-radius: 6px;
    background: transparent;
}

.email:hover {
    background: rgba(242, 14, 14, 0.1);
    transform: translateY(-2px);
    text-decoration: none;
}

.email::before {
    content: '📧';
    margin-right: 8px;
    font-size: 16px;
}

.email::after {
    content: 'Outlook';
    position: absolute;
    bottom: -25px;
    left: 50%;
    transform: translateX(-50%);
    font-size: 10px;
    opacity: 0;
    transition: opacity 0.3s ease;
    background: #333;
    color: white;
    padding: 2px 6px;
    border-radius: 3px;
    white-space: nowrap;
    pointer-events: none;
}

.email:hover::after {
    opacity: 1;
}
.nav-link {
  text-transform: uppercase;
  font-weight: bold;
  display: inline-block;
  position: relative;
  padding: 0;
  margin: 0;
  cursor: default;
  overflow: hidden;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 2px;
  background-color: #F20E0E;
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.3s ease-in-out;
}

.nav-link:hover::after {
  transform: scaleX(1);
}

/* Responsive Design */
@media (max-width: 768px) {
  .navigation {
    flex-direction: column;
    gap: 20px;
    text-align: center;
  }
  
  .profile-section {
    position: static;
    transform: none;
    order: -1; /* Met l'image en premier sur mobile */
  }
  
  .profile-image {
    width: 60px;
    height: 60px;
  }
  
  .logo-section,
  .nav-section {
    flex: none;
  }
  
  .links {
    justify-content: center;
    flex-wrap: wrap;
  }
}

@media (max-width: 480px) {
  header {
    padding-left: 20px;
    padding-right: 20px;
  }
  
  .profile-image {
    width: 50px;
    height: 50px;
  }
  
  .name {
    font-size: 1em;
  }
  
  .links {
    gap: 15px;
  }
}

/* Styles du modal About Me */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.8);
  backdrop-filter: blur(8px);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 2000;
  animation: fadeIn 0.3s ease-out;
}

.modal-content {
  background: #FFFEEF;
  border-radius: 15px;
  max-width: 800px;
  max-height: 90vh;
  width: 90%;
  overflow-y: auto;
  position: relative;
  box-shadow: 0 20px 60px rgba(242, 14, 14, 0.3);
  animation: slideUp 0.4s ease-out;
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 25px 30px;
  border-bottom: 2px solid rgba(242, 14, 14, 0.1);
  background: linear-gradient(135deg, rgba(242, 14, 14, 0.05) 0%, rgba(255, 254, 239, 0.95) 100%);
}

.modal-header h2 {
  color: #F20E0E;
  margin: 0;
  font-size: 1.8em;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.close-btn {
  background: none;
  border: none;
  font-size: 30px;
  color: #F20E0E;
  cursor: pointer;
  padding: 0;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  transition: all 0.3s ease;
}

.close-btn:hover {
  background: rgba(242, 14, 14, 0.1);
  transform: rotate(90deg);
}

.modal-body {
  padding: 30px;
}

.about-content {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 30px;
  align-items: start;
}

.about-image {
  display: flex;
  justify-content: center;
}

.about-profile-img {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  border: 4px solid #F20E0E;
  object-fit: cover;
  box-shadow: 0 10px 30px rgba(242, 14, 14, 0.3);
}

.about-text h3 {
  color: #F20E0E;
  font-size: 2em;
  margin: 0 0 5px 0;
  font-weight: bold;
}

.about-title {
  color: #666;
  font-size: 1.2em;
  margin: 0 0 20px 0;
  font-style: italic;
}

.about-description p {
  color: #333;
  line-height: 1.6;
  margin-bottom: 15px;
  text-align: justify;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
  margin: 25px 0;
}

.skill-category {
  background: rgba(242, 14, 14, 0.05);
  padding: 20px;
  border-radius: 10px;
  border-left: 4px solid #F20E0E;
}

.skill-category h4 {
  color: #F20E0E;
  margin: 0 0 15px 0;
  font-size: 1.1em;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.skill-category ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.skill-category li {
  color: #333;
  padding: 5px 0;
  position: relative;
  padding-left: 20px;
}

.skill-category li::before {
  content: '▶';
  position: absolute;
  left: 0;
  color: #F20E0E;
  font-size: 0.8em;
}

.contact-cta {
  background: linear-gradient(135deg, #F20E0E 0%, #ff4444 100%);
  color: white;
  padding: 25px;
  border-radius: 12px;
  text-align: center;
  margin-top: 25px;
}

.contact-cta p {
  margin: 0 0 15px 0;
  font-size: 1.1em;
  color: white !important;
}

.cta-btn {
  background: white;
  color: #F20E0E;
  border: none;
  padding: 12px 25px;
  border-radius: 25px;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.cta-btn:hover {
  background: rgba(255, 255, 255, 0.9);
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

/* Animations */
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes slideUp {
  from {
    transform: translateY(50px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

/* Responsive pour le modal */
@media (max-width: 768px) {
  .about-content {
    grid-template-columns: 1fr;
    text-align: center;
    gap: 20px;
  }
  
  .about-profile-img {
    width: 150px;
    height: 150px;
  }
  
  .modal-content {
    width: 95%;
    margin: 10px;
  }
  
  .modal-header,
  .modal-body {
    padding: 20px;
  }
  
  .skills-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 480px) {
  .modal-header h2 {
    font-size: 1.4em;
  }
  
  .about-text h3 {
    font-size: 1.5em;
  }
  
  .about-profile-img {
    width: 120px;
    height: 120px;
  }
}
</style>


