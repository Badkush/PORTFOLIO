<template>
    <Header />
    <Home />
    <Work />
    <Contact />
    <Footer />
</template>

<script setup>
import Header from './header.vue'; // Importation du composant Header
import Home from './Home.vue'; // Importation du composant Home
import Work from './assets/Work.vue'; // Importation du composant Work
import Contact from './assets/Contact.vue'; // Importation du composant Contact
import Footer from './Footer.vue'; // Importation du composant Footer
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100..900;1,100..900&display=swap');

/* Styles globaux pour l'application */
body {
  font-family: 'Roboto', sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  padding-top: 120px; /* Espace pour le header fixe */
  padding-bottom: 220px; /* Espace augmenté pour le footer fixe */
}

/* Reset global pour éviter les conflits */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Assurer que le contenu principal commence après le header */
main {
  padding-top: 0;
}
</style>

<!--
  Le dépôt Git a été initialisé avec succès.
  Vous pouvez maintenant commencer à suivre vos fichiers avec Git.

  Commandes utiles :
  - git add <fichier> : Ajouter un fichier au suivi
  - git commit -m "Message" : Enregistrer les modifications
  - git push : Pousser les modifications vers le dépôt distant
-->

git add .
git commit -m "Premier commit"
git remote add origin TON_URL_GITHUB