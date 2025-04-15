<template>

    <!-- Je vais créer un composant Header qui va contenir le nom et le métier de la personne ainsi que les liens vers les différentes sections de la page. -->
    <!-- Je vais utiliser le :style inline pour le header et le nav pour que ça soit plus simple à lire et à comprendre. -->
    <header :style="{ backgroundColor: 'transparent', fontSize: '23px', lineHeight: '23px', fontWeight: 'bold', letterSpacing: '-1.5px', position: 'fixed', top: '0px', width: '100%', backdropFilter: 'blur(10px)' }">

        <nav :style="{ paddingTop: '70px', display: 'flex', justifyContent: 'space-between', alignItems: 'center' }">

            <section :style="{ display: 'flex', flexDirection: 'column', paddingLeft: '80px' }">

                <a :href="'#'">
                    <p>{{ name }}<br>
                    <span :style="{ fontWeight: 'normal', lineHeight: '23px', fontSize: '23px' }">{{ metier }}</span>
                    </p>                   
                </a>

            </section>

            <section :style="{ display: 'flex', alignItems: 'center', paddingRight: '80px' }">

                <ul :style="{ display: 'flex', listStyle: 'none', textTransform: 'uppercase', textDecoration: 'none', gap: '50px' }">

                    <!-- La directive v-for est utilisée pour itérer (répéter) sur le tableau de liens et créer un élément de liste pour chaque lien. -->
                    <!-- La directive :key est utilisée pour donner une clé unique à chaque élément de la liste, ce qui aide Vue à suivre les éléments lors du rendu. -->
                    <!-- La directive :href est utilisée pour lier l'URL du lien à la propriété url de chaque objet dans le tableau liens. -->
                    <li v-for="lien in liens" :key="lien.nom">
                        <a :href="lien.url">{{ lien.nom }}</a>
                    </li>

                    <!-- Utilisation de la directive v-on pour lier un événement de clic à la fonction toggleDarkMode -- -->
                <button @click="toggleDarkMode" :class="{ backgroundColor: isDarkMode ? '#333' : '#fffeef', color: isDarkMode ? '#fffeef' : '#f20e0e' }">

                <!-- Utilisation de la directive v-if pour afficher une icône différente en fonction du mode sombre -->
                <span v-if="isDarkMode">☀️</span>
                <span v-else>🌙</span>
                
                </button>

                </ul>

            </section>
            
        </nav>

    </header>

</template>

<script setup lang="ts">

// Importation des modules nécessaires pour la réactivité
import { ref } from 'vue';

// je vais utiliser le defineProps pour définir les props que je vais passer au composant Header
defineProps<{
    name: string,
    metier: string,
    liens: { nom: string, url: string }[]
}>();

// Je vais utiliser le ref pour créer une variable réactive qui va contenir l'état du darkmode
const isDarkMode = ref(false);

// Je vais créer une fonction qui va changer l'état du darkmode
// Je vais utiliser le v-on pour lier l'événement de clic à la fonction toggleDarkMode
function toggleDarkMode() {
    isDarkMode.value = !isDarkMode.value;
}

</script>

<style scoped>

/* Je vais utiliser le scoped pour que mes styles ne s'appliquent qu'à ce composant */
nav a {
    text-decoration: none;
    color: #f20e0e;
    font-size: 25px;
    margin: '0px';
}

a:hover {
    text-decoration: underline;
}

button {
    background-color: transparent;
    border: none;
    cursor: pointer;
    font-size: 25px;
    color: #f20e0e;
}

</style>
