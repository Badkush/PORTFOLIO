<template>
    
    <!-- Je vais utiliser le :style inline pour le header et le nav pour que ça soit plus simple à lire et à comprendre. -->
    <footer class="footer-container" :class="{ dark: isDarkMode }">

        <section>

            <div>

                <!-- La directive v-bind est utilisée pour lier les propriétés du composant aux props passées depuis le parent. -->
                <p class="date">{{ footerText }}</p>
                <p class="prenom">{{ createdBy }}</p>
            </div>

        </section>
        
        <section class="footer-links">

            <ul class="footer-links">

                <!-- La directive v-for est utilisée pour itérer sur le tableau de liens et créer un élément de liste pour chaque lien. -->
                <!-- La directive :key est utilisée pour donner une clé unique à chaque élément de la liste, ce qui aide Vue à suivre les éléments lors du rendu. -->
                <li v-for="(link, index) in socialLinks" :key="index">
                    <a :href="link.url" target="_blank" rel="noopener noreferrer">
                        {{ link.name }}
                    </a>
                </li>
            </ul>

            <!-- Utilisation de la directive v-on pour lier un événement de clic à la fonction toggleDarkMode -- -->
            <button @click="toggleDarkMode" :style="{ backgroundColor: isDarkMode ? '#333' : '#fffeef', color: isDarkMode ? '#fffeef' : '#f20e0e' }">

                <!-- Utilisation de la directive v-if pour afficher une icône différente en fonction du mode sombre -->
                <span v-if="isDarkMode">☀️</span>
                <span v-else>🌙</span>

            </button>

        </section>

    </footer>

</template>

<script setup lang="ts">

// Importation des modules nécessaires pour la réactivité
import { ref } from 'vue';

// Importation de la fonction defineProps pour définir les propriétés du composant
// Le composant Resaux reçoit trois propriétés : footerText, createdBy et socialLinks
defineProps<{
    footerText: string;
    createdBy: string;
    socialLinks: { name: string; url: string }[];
}>();

const isDarkMode = ref(false);

function toggleDarkMode() {
    isDarkMode.value = !isDarkMode.value;
}

</script>

<style scoped>

/* Je vais utiliser le scoped pour que mes styles ne s'appliquent qu'à ce composant */
.footer-container {
    display: flex;
    justify-content: space-between;
    padding-top: 200px;
    background-color: #fffeef;
    color: #f20e0e;
    text-align: center;
    font-family: 'Roboto', sans-serif;
    
    /* Animation d'apparition */
    animation: fadeIn 2s ease-in-out; 
}

/* mon opacité de début (from) et celui de fin (to) */
@keyframes fadeIn {
    from {
        opacity: 100%;
        transform: translateY(20px);
    }
    to {
        opacity: 10%;
        transform: translateY(0);
    }
}

.prenom {
    margin: 0px;
    font-size: 28px;
    line-height: 30px;
    text-transform: uppercase;
    letter-spacing: -1px;
    text-decoration: underline;
    color: #f20e0e;
}

.date {
    margin: 0px;
    font-size: 28px;
    line-height: 30px;
    text-transform: uppercase;  
    letter-spacing: -1px;
    color: #f20e0e;
}

/* J'ajuste mes liens avec gap */
.footer-links {
    list-style: none;
    display: flex;
    align-items: center;
    gap: 20px;
}

.footer-links a {
    color: #f20e0e;
    text-decoration: none;

    /* Je vais utiliser le transition pour que mes liens aient une animation de transition */
    transition: color 0.3s ease;

    font-size: 25px;
    line-height: 25px;
    text-transform: uppercase;
    padding: 10px 20px;
    border-top-left-radius: 20px, #f20e0e;
    border-radius: 5px 5px 20px 10px;
    border-top: 10px #f20e0e solid;
    border-left: 5px #f20e0e solid;
    background-color: #fffeef;
    box-shadow: 0 10px 15px #f20e0e;
}

.footer-links a:hover {
    color: #f20e0e;
    font-weight: bold;
}

.ter-links li {
    display: flex;
    align-items: center;
    justify-content: center;
}

button {
    background-color: transparent;
    border: none;
    cursor: pointer;
    font-size: 25px;
    margin-left: 20px;
}

/* styles du darkMode */
.footer-container.dark {
    margin: 0px;
    background-color: #333;
    color: #f20e0e;
}

.footer-links a.dark {
    color: #f20e0e;
    text-decoration: none;
    transition: color 0.3s ease;
    font-size: 25px;
    line-height: 25px;
    text-transform: uppercase;
    padding: 10px 20px;
    border-top-left-radius: 20px, #f20e0e;
    border-radius: 5px 5px 20px 10px;
    border-top: 10px #f20e0e solid;
    border-left: 5px #f20e0e solid;
    background-color: #333;
    box-shadow: 0 5px 10px #f20e0e;
}

.footer-links a.dark:hover {
    color: #f20e0e;
    font-weight: bold;
}

</style>