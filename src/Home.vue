<template>
    <section>
        <div class="container">
            <h1 class="name">maxime cuche</h1>
            <div class="presentation" style="margin: 0; padding: 0;">
                <p 
                    ref="contentElement"
                    class="content" 
                    :class="{ 'animate-in': isVisible }"
                    style="margin: 0; padding: 0;"
                >
                    Je suis un développeur web et mobile indépendant basé<br> à Mercues travaillant pour des <br>clients particuliers dans le Lot.
                </p>
                <a href="mailto:maxcuche46@gmail.com">
                    <p class="mail">maxcuche46@gmail.com</p>
                </a>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const contentElement = ref(null)
const isVisible = ref(false)
let observer = null

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          isVisible.value = true
          // Optionnel : arrêter d'observer une fois l'animation déclenchée
          // observer.unobserve(entry.target)
        }
      })
    },
    {
      threshold: 0.3, // L'animation se déclenche quand 30% de l'élément est visible
      rootMargin: '0px 0px -50px 0px' // Déclenche un peu avant que l'élément soit complètement visible
    }
  )
  
  if (contentElement.value) {
    observer.observe(contentElement.value)
  }
})

onUnmounted(() => {
  if (observer) {
    observer.disconnect()
  }
})
</script>

<style scoped>
section {
  background-color: #FFFEEF;
  color: #F20E0E;
  font-weight: 500;
  text-align: center;
  min-height: 100vh; /* Hauteur complète de la fenêtre */
  padding-top: 0; /* Supprime le padding-top car il est géré globalement */
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh; /* Hauteur complète pour le centrage */
  padding-top: 120px; /* Compensation pour le header fixe */
}
h1.name {
  font-weight: 350;
  font-size: 250px;
  font-family: 'Roboto', sans-serif;
  line-height: 250px;
  letter-spacing: -5px;
  text-transform: capitalize;
  
}
.presentation {
  max-width: 800px; /* Limite la largeur du texte pour une meilleure lisibilité */
}
p.content {
  font-size: 30px;
  font-weight: 100;
  font-family: 'Arial Narrow Bold', sans-serif;
  /* État initial - élément caché à droite */
  transform: translateX(100%);
  transition: all 1.5s ease-out;
}

/* État animé quand l'élément devient visible */
p.content.animate-in {
  transform: translateX(0);
  opacity: 1;
}
a {
  text-decoration: none;
}
p.mail {
  font-size: 30px;
  font-weight: bold;
  text-decoration: solid underline;
  color: #F20E0E;
  margin-top: 50px;
  margin-bottom: 0px;
}
</style>