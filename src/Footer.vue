<template>
  <footer class="footer">
    <div class="footer-content">
      <div class="footer-section">
        <h3 class="footer-title">Maxime Cuche</h3>
        <p class="footer-subtitle">Développeur Web & Mobile</p>
        <p class="footer-location">📍 Mercues, Lot (46)</p>
      </div>

      <div class="footer-section">
        <h4>Contact</h4>
        <div class="contact-links">
          <a href="mailto:maxcuche46@gmail.com" class="footer-link">
            <svg viewBox="0 0 24 24" fill="currentColor">
              <path d="M20 4H4c-1.1 0-1.99.9-1.99 2L2 18c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
            </svg>
            Email
          </a>
          <a href="https://github.com/Badkush" target="_blank" class="footer-link">
            <svg viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
            </svg>
            GitHub
          </a>
        </div>
      </div>

      <div class="footer-section">
        <h4>Services</h4>
        <ul class="services-list">
          <li>Sites Web Vitrine</li>
          <li>Applications Web</li>
          <li>Design UI/UX</li>
          <li>Applications Mobile</li>
        </ul>
      </div>

      <div class="footer-section">
        <h4>Navigation</h4>
        <nav class="footer-nav">
          <a href="#home" class="nav-link" @click="scrollToSection('home')">Accueil</a>
          <a href="#work" class="nav-link" @click="scrollToSection('work')">Travaux</a>
          <a href="#contact" class="nav-link" @click="scrollToSection('contact')">Contact</a>
        </nav>
      </div>
    </div>

    <div class="footer-bottom">
      <div class="footer-bottom-content">
        <p>© 2025 Maxime Cuche - Développeur Web & Mobile. Tous droits réservés.</p>
        <p class="made-with">
          <strong>Vue.js</strong>
        </p>
      </div>
    </div>
  </footer>
</template>

<script setup>
// Fonction pour faire défiler vers une section
const scrollToSection = (sectionId) => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({
      behavior: 'smooth',
      block: 'start'
    })
  } else {
    // Si l'élément n'est pas trouvé, scroll vers le haut
    window.scrollTo({
      top: 0,
      behavior: 'smooth'
    })
  }
}
</script>

<style scoped>
.footer {
  background: rgba(255, 254, 239, 0.75);
  color: #F20E0E;
  font-family: 'Roboto', sans-serif;
  margin-top: 0;
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 999;
  box-shadow: 0 -4px 20px rgba(242, 14, 14, 0.15);
  backdrop-filter: blur(20px);
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px 20px 15px;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 20px;
}

.footer-section h3,
.footer-section h4 {
  margin-bottom: 12px;
  font-weight: bold;
}

.footer-title {
  font-size: 1.6rem;
  color: #F20E0E;
  margin-bottom: 6px;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
  text-shadow: 0 1px 2px rgba(255, 254, 239, 0.8);
}

.footer-subtitle {
  font-size: 1rem;
  color: #F20E0E;
  margin-bottom: 8px;
  font-weight: 300;
  opacity: 0.8;
}

.footer-location {
  color: #F20E0E;
  font-size: 0.95rem;
  display: flex;
  align-items: center;
  gap: 5px;
  opacity: 0.9;
}

.footer-section h4 {
  font-size: 1.1rem;
  color: #F20E0E;
  border-bottom: 2px solid #F20E0E;
  padding-bottom: 5px;
  margin-bottom: 12px;
  font-weight: bold;
  text-shadow: 0 1px 2px rgba(255, 254, 239, 0.6);
}

.contact-links {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.footer-link {
  display: flex;
  align-items: center;
  gap: 10px;
  color: #F20E0E;
  text-decoration: none;
  transition: all 0.3s ease;
  padding: 8px 0;
  font-weight: 500;
  opacity: 0.8;
}

.footer-link:hover {
  opacity: 1;
  transform: translateX(5px);
}

.footer-link svg {
  width: 18px;
  height: 18px;
  transition: transform 0.3s ease;
}

.footer-link:hover svg {
  transform: scale(1.2);
}

.services-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.services-list li {
  padding: 4px 0;
  color: #F20E0E;
  position: relative;
  padding-left: 20px;
  transition: opacity 0.3s ease;
  opacity: 0.8;
}

.services-list li:before {
  content: "▶";
  position: absolute;
  left: 0;
  color: #F20E0E;
  font-size: 0.8rem;
  top: 8px;
}

.services-list li:hover {
  opacity: 1;
  cursor: default;
}

.footer-nav {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.nav-link {
  color: #F20E0E;
  text-decoration: none;
  transition: all 0.3s ease;
  padding: 5px 0;
  position: relative;
  font-weight: 500;
  opacity: 0.8;
}

.nav-link:hover {
  opacity: 1;
  padding-left: 10px;
}

.nav-link:before {
  content: "";
  position: absolute;
  left: -15px;
  top: 50%;
  transform: translateY(-50%);
  width: 0;
  height: 2px;
  background: #F20E0E;
  transition: width 0.3s ease;
}

.nav-link:hover:before {
  width: 8px;
}

.footer-bottom {
  background: rgba(242, 14, 14, 0.05);
  border-top: 1px solid rgba(242, 14, 14, 0.15);
}

.footer-bottom-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 10px 20px;
  text-align: center;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 8px;
}

.footer-bottom p {
  margin: 0;
  color: #F20E0E;
  font-size: 0.9rem;
  opacity: 0.9;
}

.made-with {
  display: flex;
  align-items: center;
  gap: 5px;
  font-size: 0.9rem !important;
}

.heart {
  color: #F20E0E;
  animation: heartbeat 2s infinite;
  font-size: 1rem;
}

@keyframes heartbeat {
  0%, 50%, 100% { transform: scale(1); }
  25%, 75% { transform: scale(1.1); }
}

.made-with strong {
  color: #F20E0E;
  font-weight: 600;
}

/* Responsive Design */
@media (max-width: 768px) {
  .footer-content {
    grid-template-columns: 1fr;
    gap: 15px;
    padding: 20px 20px 10px;
    text-align: center;
  }
  
  .footer-bottom-content {
    flex-direction: column;
    text-align: center;
    gap: 10px;
  }
  
  .contact-links {
    align-items: center;
  }
  
  .footer-nav {
    align-items: center;
  }
  
  .nav-link:hover {
    padding-left: 0;
  }
  
  .nav-link:before {
    display: none;
  }
}

@media (max-width: 480px) {
  .footer-content {
    padding: 30px 15px 15px;
  }
  
  .footer-title {
    font-size: 1.5rem;
  }
  
  .footer-section h4 {
    font-size: 1.1rem;
  }
}

/* Animation d'entrée */
.footer-section {
  opacity: 0;
  animation: fadeInUp 0.6s ease forwards;
}

.footer-section:nth-child(1) { animation-delay: 0.1s; }
.footer-section:nth-child(2) { animation-delay: 0.2s; }
.footer-section:nth-child(3) { animation-delay: 0.3s; }
.footer-section:nth-child(4) { animation-delay: 0.4s; }

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