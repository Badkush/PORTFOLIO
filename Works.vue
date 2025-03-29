<template>
    <section class="slider-container">

        <!-- Utilisation de v-bind pour lier les propriétés du composant aux props passées depuis le parent. -->
        <button class="prev" @click="prevSlide">❮</button>

        <!-- Utilisation de TransitionGroup pour gérer les transitions entre les diapos -->
        <TransitionGroup name="slide" tag="div" class="slider">

            <!-- Utilisation de v-bind pour lier les propriétés du composant aux props passées depuis le parent. -->
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

        <button class="next" @click="nextSlide">❯</button>
    </section>
</template>

<script setup lang="ts">

// Importation des modules nécessaires pour la réactivité
import { ref, computed } from 'vue';

// Importation de la fonction defineProps pour définir les propriétés du composant
defineProps<{
    card: 'card'
    ls: 'la socketterie'
    NFT: 'NFT'
    gaming: 'gaming'
    art: 'art'
    troisD: 'troisD'
}>();

// État réactif pour la diapositive actuelle
const currentSlide = ref(0);

// Tableau des diapos à afficher dans le carrousel
const slides = ref(['card', 'la socketterie', 'NFT', 'gaming', 'art', 'troisD']);

// Nombre de diapos à afficher
const slidesToShow = 3;

// Calcul des diapos visibles en fonction de la diapositive actuelle.
// La propriété calculée visibleSlides calcule les diapos qui doivent être visibles en fonction de l'index currentSlide et du nombre de diapositives à afficher.
// La fonction computed est utilisée pour créer une propriété calculée qui dépend de la valeur de currentSlide et slidesToShow.
// Elle renvoie un tableau contenant les diapos visibles en fonction de l'index de la diapositive actuelle et du nombre de diapos à afficher.
// La fonction slice est utilisée pour extraire une partie du tableau slides en fonction de l'index de la diapositive actuelle et du nombre de diapos à afficher.
// Elle utilise la méthode slice pour extraire une partie du tableau slides en fonction de l'index de la diapositive actuelle et du nombre de diapos à afficher.
// La méthode % est utilisée pour gérer le cas où l'index de la diapositive actuelle dépasse la longueur du tableau slides, en revenant au début du tableau. 
// Si l'index de la diapositive actuelle est inférieur à l'index de fin, elle renvoie simplement la tranche du tableau.
// Sinon, elle renvoie deux tranches du tableau : une à partir de l'index de la diapositive actuelle jusqu'à la fin du tableau, et l'autre du début du tableau jusqu'à l'index de fin.
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
.slider-container {
    position: relative;
    width: 600px;
    height: 400px;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
}

.slider {
    display: flex;
    gap: 10px;
    position: relative;
    width: 100%;
    height: 100%;
}

.slide {
    flex: 1 0 calc(100% / 3 - 10px); /* J'ajuste mes diapos avec gap */
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #f0f0f0;
    border: 1px solid #ccc;
    text-align: center;
    font-size: 1.5rem;
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

button {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background-color: rgba(0, 0, 0, 0.5);
    color: white;
    border: none;
    padding: 10px;
    cursor: pointer;
    z-index: 10;
}

button.prev {
    left: 10px;
}

button.next {
    right: 10px;
}

button:hover {
    background-color: rgba(0, 0, 0, 0.8);
}
</style>