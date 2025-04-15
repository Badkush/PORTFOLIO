<template>

    <!-- La directive v-bind est utilisée pour lier les propriétés du composant aux props passées depuis le parent. -->
    <p>{{ titre }}</p>

    <!-- Utilisation de @submit.prevent pour empêcher le rechargement de la page lors de la soumission du formulaire -->
    <!-- Utilisation de v-on pour lier dynamiquement les attributs des éléments HTML aux propriétés du champ de formulaire -->
    <form @submit.prevent="handleSubmit" class="form-container">
        
        <!-- Utilisation de v-for pour itérer sur les champs de formulaire définis dans formFields et créer un champ pour chaque élément -->
        <!-- La directive :key est utilisée pour donner une clé unique à chaque élément de la liste, ce qui aide Vue à suivre les éléments lors du rendu. -->
        <div v-for="(field, index) in formFields" :key="index" class="form-group">

            <label :for="field.name">{{ field.label }}</label>

            <!-- Utilisation de v-if pour afficher le bon type de champ en fonction de la définition du champ -->
            <!-- Utilisation de v-model pour lier la valeur du champ de formulaire à l'objet formData -->
            <input
                v-if="field.type === 'text'"
                :type="field.type"
                :id="field.name"
                v-model="formData[field.name]"
                :placeholder="field.placeholder"
            />

            <!-- Utilisation de v-else-if pour gérer les différents types de champs de formulaire (input, textarea, select) -->
            <textarea
                v-else-if="field.type === 'textarea'"
                :id="field.name"
                v-model="formData[field.name]"
                :placeholder="field.placeholder"
            ></textarea>

            <select
                v-else-if="field.type === 'select'"
                :id="field.name"
                v-model="formData[field.name]"
            >
                
                <option v-for="option in field.options" :key="option" :value="option">
                    {{ option }}
                </option>
                <option disabled value="">{{ field.placeholder }}</option>
                
            </select>

        </div>

        <button>Envoyé</button>

    </form>

</template>

<script setup lang="ts">

// Importation des modules nécessaires pour la réactivité
import { reactive } from 'vue';

// Importation de la fonction defineProps pour définir les propriétés du composant  
defineProps<{
    titre: string;
}>();


// Le tableau formFields définit les champs de manière dynamique, y compris leur nom, leur étiquette, leur type et d'autres propriétés telles que l'espace réservé ou les options.
const formFields = [
    { name: 'name', label: 'Nom complet', type: 'text', placeholder: 'Entrer votre nom' },
    { name: 'email', label: 'Votre email', type: 'text', placeholder: 'Entrer votre email' },
    { name: 'message', label: 'Votre message', type: 'textarea', placeholder: 'Entrer votre message' },
    {
        name: 'category',
        label: 'Réalisations',
        type: 'select',
        options: ['3d', 'Card', 'Gaming', 'Art', 'NFT', 'La socketterie'],
        placeholder: 'Sélectionner un produit',
    },
];

// Objet réactif pour stocker les données du formulaire
const formData = reactive({
    name: '',
    email: '',
    message: '',
    category: '',
});



// Fonction pour gérer la soumission du formulaire
const handleSubmit = () => {
    console.log(formData);
    alert('Message envoyé!');
};

</script>

<style scoped>

/* Je vais utiliser le scoped pour que mes styles ne s'appliquent qu'à ce composant */
p {
    text-align: center;
    margin-bottom: 120px;
    font-size: 80px;
    color: #f20e0e;
    letter-spacing: -5px;
    line-height: '150px';
    text-transform: uppercase;
    text-shadow: 1px 1px 2px #473030;
}

/* Style de mon formulaire */
.form-container {
    display: flex;
    flex-direction: column;
    gap: 2rem;
    max-width: 400px;
    margin: 0 auto;
}

.form-group {
    display: flex;
    flex-direction: column;
}

label {
    font-weight: bold;
    margin-bottom: 0.5rem;
}

input,
textarea,
select {
    padding: 0.5rem;
    border: 1px solid #f20e0e;
    border-radius: 15px;
    font-size: 1rem;
}

button {
    padding: 15px;
    background-color: #fff;
    border: none;
    border-radius: 15px;
    cursor: pointer;
    font-size: 1rem;
    font-weight: bold;
    color: #f20e0e;
    text-transform: uppercase;
    border: #f20e0e solid 2px;
}

/* Style de mon bouton au survol */
button:hover {
    background-color: #f20e0e;
    color: #fffeef;
}

</style>