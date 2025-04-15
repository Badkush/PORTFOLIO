<template>
        
        <!-- La directive v-on est utilisée pour lier les propriétés de style CSS à l'élément. -->
        <button class="prev" @click="prevSlide">❮</button>

    <section class="slider-container">

        <!-- Utilisation de TransitionGroup pour gérer les transitions entre les diapos -->
        <!-- La directive :style est utilisée pour appliquer un style dynamique à l'élément, en fonction du nombre de diapos à afficher. -->
        <TransitionGroup name="slide" tag="div" class="slider" :style="{ width: `${slidesToShow * 100}%` }">

            <!-- La directive v-for est utilisée pour itérer (répéter) sur les diapos visibles et afficher chaque diapositive. -->
            <!-- La clé est définie sur l'index de la diapo pour assurer les transitions. -->
            <!-- La propriété :key est utilisée pour identifier chaque diapositive de manière unique. -->         
            <div
                class="slide"
                v-for="(item, index) in visibleSlides"
                :key="index">
                {{ item }}                        
            </div>

        </TransitionGroup>

    </section>

        <button class="next" @click="nextSlide">❯</button>

</template>

<script setup lang="ts">

// Importation des modules nécessaires pour la réactivité
import { ref, computed } from 'vue';

// Importation de la fonction defineProps pour définir les propriétés du composant
defineProps<{
    card: string;
    ls: string;
    NFT: string;
    gaming: string;
    art: string;
    troisD: string;
}>();

// État réactif pour la diapositive actuelle
const currentSlide = ref(0);

// Tableau des diapos à afficher dans le carrousel
const slides = ref(['card', 'la socketterie', 'NFT', 'gaming', 'art', 'troisD']);

// Nombre de diapos à afficher
const slidesToShow = 3;

// La fonction computed est utilisée pour créer une propriété calculée qui dépend de la diapositive actuelle
// La propriété calculée visibleSlides calcule les diapositives qui doivent être visibles en fonction de l'index currentSlide et du nombre de diapositives à afficher.
// Elle utilise la méthode slice pour extraire une partie du tableau slides en fonction de l'index de la diapositive actuelle et du nombre de diapositives à afficher.
// La logique de calcul des diapos visibles est gérée ici

const visibleSlides = computed(() => {
    const start = currentSlide.value;
    const end = (currentSlide.value + slidesToShow) % slides.value.length;
    if (start < end) {
        return slides.value.slice(start, end);
    } else {
        return [...slides.value.slice(start), ...slides.value.slice(0, end)];
    }
});

// Ma fonction pour aller à la diapositive précédente
const prevSlide = () => {
    currentSlide.value =
        (currentSlide.value - 1 + slides.value.length) % slides.value.length;
};

// Ma fonction pour aller à la diapositive suivante
const nextSlide = () => {
    currentSlide.value =
        (currentSlide.value + 1) % slides.value.length;
};

</script>

<style scoped>

/* Je vais utiliser le scoped pour que mes styles ne s'appliquent qu'à ce composant */
.slider-container {
    width: 1000px;
    height: 500px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    margin: 0 auto;
    margin: 300px;
}

/* J'ajuste mes diapos avec gap */
.slider {
    display: flex;
    gap: 50px;
    position: relative;
    width: 100%;
    height: 100%;
}

.slide {
    flex: 1 0 calc(100% / 3 - 10px); 
    width: calc(100% / 3 - 10px);   
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    font-size: 30px;
    border: 3px solid #f20e0e;  
    border-radius: 20px 40px 120px 20px;
    box-shadow: 0px 0px 30px #f20e0e;
    text-shadow: 1px 1px 2px #333;
}

/* Le style dynamique de mon box shadow au survol */
.slide:hover {
    box-shadow: 20px 10px 40px #333;
    transform: scale(1.05);
    transition: all 0.3s ease-in-out;
    background-color: #f20e0e;
    color: #fffeef;
    font-size: 30px;
    font-weight: bold;
    text-transform: uppercase;
    letter-spacing: -1px;
    text-shadow: 1px 1px 2px #333;
}

/* Les styles de mes transitions */
.slide-enter-active,
.slide-leave-active {
    transition: transform 0.5s ease, opacity 0.5s ease;
}

.slide-enter-from {
    transform: translateX(100%);
    opacity: 0;
}

.slide-leave-to {
    transform: translateX(-100%);
    opacity: 0;
}

/* Les styles de mes boutons */
button.prev {
    transform: translateY(-50%);
    background-color: #f20e0e;
    color: #fffeef;
    border-radius: 100%;
    border: none;
    padding: 20px;
    cursor: pointer;
}

button.next {
    transform: translateY(-50%);
    background-color: #f20e0e;
    color: #fffeef;
    border-radius: 100%;
    padding: 20px;
    cursor: pointer;
    border: none;
}

button:hover {
    background-color: #333;
    color: #f20e0e;
    border-radius: 100%;
    padding: 20px;
    cursor: pointer;
}

</style>