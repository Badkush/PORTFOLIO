<script setup lang="ts">

  // Importation de mes composants et des modules nécessaires pour la réactivité
  import { ref } from 'vue';
  import { UseElementVisibility } from '@vueuse/components'
  import Header from './components/Navigation.vue'
  import Works from './components/Works.vue'
  import Form from './components/Form.vue'
  import Resaux from './components/Resaux.vue'
  
  // Mes différentes variables et constantes
    const infos = {
        name: 'MAXIME CUCHE',
        metier: 'Développeur web',
        identité: 'Maxime Cuche',     
        propos: `Je suis un développeur web passionné
        par la création de sites internet et de maquettes graphiques 
        basé à Mercuès dans le LOT.`,
        email: 'maxcuche@gmail.com',
        footer: '© 2025 - Tous droits réservés',
        createdBy: 'Crée par Maxime Cuche',
        titre: 'Contactez-moi',
        liens: [
            { nom: 'ACCUEIL', url: '#' },
            { nom: 'REALISATIONS', url: '#' },
            { nom: 'CONTACT', url: '#' },
            { nom: 'RESAUX', url: '#' },
        ]
    }

    const presentation = ref(
        `Depuis toujours, je suis passionné par l'informatique et l'IA que je découvre à travers diverses expériences en autodidact. Depuis peu, j’ai le projet d’orienter ma carrière en tant que développer web.
        En effet, depuis l’époque de ma carrière de paysagiste, j’ai toujours eu le goût du travail d'équipe ainsi que l’exigence de la qualitée. Que ce soit lors des travaux pratiques ou lors des projets auquel j'ai participé, j’apprécie le fait de pouvoir assouvir ma curiositée.
        A la suite de ma reconversion professionnel, j’ai logiquement choisi de suivre une formation de développeur web en accord avec ma passion de la programmation, de l’outil informatique et de l'élaboration de maquettes graphiques.
        Cette formation a complètement et totalement confirmé que je voulais poursuivre dans cette voie. Je suis déterminé et conscient que ce métier est en perpétuel évolution. Je suis sur qu'il correspond parfaitement à mes qualitées.
        Je possède des compétences techniques solides et je maitrise les langages HTML, CSS, JavaScript, ainsi que des frameworks comme Vue.js. Je suis quelqu'un de créatif capable de concevoir des interfaces utilisateur attrayantes et intuitives
        Je sait résoudre des problèmes parfois complex pour identifier et corriger les bugs rapidement et efficacement. J'aime apprendre continuelement car le domaine du développement web évolue constamment, donc rester à jour avec les dernières technologies est tendance et vital.
        J'ai un esprit collaboratif capable de communiquer et collaborer facilement pour respecter les délais et prioriser les taches. Je suis actuellement en recherche d'emploi et je suis ouvert à toutes propositions. Je suis disponible pour un entretien à votre convenance.`
    )

    const travaux = {
      card: "card" as const, 
      ls: 'la socketterie' as const, 
      NFT: 'NFT' as const, 
      gaming: 'gaming' as const,
      art: 'art' as const,
      troisD: 'troisD' as const
    }

    const socialLinks = [
      { name: 'Instagram', url: 'https://www.instagram.com/maximecuche/' },
      { name: 'Facebook', url: 'https://www.facebook.com/maximecuche' },
      { name: 'GitHub', url: 'https://github.com/' },
    ]

</script>

<template>

    <Header :name="infos.name" :metier="infos.metier" :liens="infos.liens" />
    
    <!-- Je vais utiliser le :style inline pour que ça soit plus simple à lire et à comprendre. -->
    <main :style="{ backgroundColor: '#fffeef', color: '#f20e0e', fontSize: '23px', lineHeight: '23px', letterSpacing: '-1.5px', padding: '80px' }">

        <section :style="{ display: 'flex', flexDirection: 'column', alignItems: 'center', textTransform: 'uppercase', textAlign: 'center' }">

            <h1 :style="{ paddingTop: '400px', paddingBottom: '80px', margin: '0px', fontSize: '300px' , lineHeight: '300px', fontWeight: '300px', letterSpacing: '-7.5px', textTransform: 'none' }">{{ infos.identité }}</h1>
            <p :style="{ fontSize:'27px', lineHeight:'30px', fontWeight: '400px', letterSpacing:'-2px', whiteSpace: 'pre-wrap', margin: '0px' }">{{ infos.propos }}</p>
            <a :href="'mailto:' + infos.email" :style="{ color: '#f20e0e', fontSize: '24px', fontWeight: '500px', lineHeight: '24px', paddingTop: '120px', paddingBottom: '260px' }">{{ infos.email }}</a>

        </section>

        <!-- J'utilise un composant intégré dans vue pour mon animation de texte-->
        <UseElementVisibility v-slot="{ isVisible }">

          <section :class="{ slide: isVisible }" :style="{ fontWeight: '400px', fontSize: '21px', paddingLeft: '250px', paddingRight: '250px', textShadow: '1px 1px 2px #473030' }">

            <article>
              <p :style="{ lineHeight: '25px', fontSize: '25px', whiteSpace: 'pre-wrap' }">{{ presentation }}</p>
            </article>

          </section>

        </UseElementVisibility>

      <section :style="{ display: 'flex', justifyContent: 'center', alignItems: 'center', textTransform: 'uppercase', textAlign: 'center' }">
        <Works v-bind="travaux" />
      </section>

      <section>
        <Form :name="infos.name" :liens="infos.liens" :titre="infos.titre" />
      </section>
     
    </main>

    <footer>
        <Resaux :footerText="infos.footer" :createdBy="infos.createdBy" :socialLinks="socialLinks" />
    </footer>

</template>      

<style scoped>

/* Je vais utiliser le scoped pour que mes styles ne s'appliquent qu'à ce composant */
/* Importation de la font */
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap');

/* Application de la font à l'ensemble de mon application */
body {
    font-family: 'Roboto condensed', sans-serif;
}

/* Animation d'apparition et définition de la durée*/
.slide {
  animation-duration: 3s;
  animation-name: slideInRight;
}

@keyframes slideInRight {
  from {
    transform: translate3d(100%, 0, 0);
    visibility: visible;
  }

  to {
    transform: translate3d(0, 0, 0);
  }
}

@keyframes bounceInUp {
  from,
  60%,
  75%,
  90%,
  to {
    animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
  }

  from {
    opacity: 0;
    transform: translate3d(0, 3000px, 0) scaleY(5);
  }

  60% {
    opacity: 1;
    transform: translate3d(0, -20px, 0) scaleY(0.9);
  }

  75% {
    transform: translate3d(0, 10px, 0) scaleY(0.95);
  }

  90% {
    transform: translate3d(0, -5px, 0) scaleY(0.985);
  }

  to {
    transform: translate3d(0, 0, 0);
  }
}

@keyframes slidein {
  from {
    margin-left: 100%;
    width: 300%;
  }

  to {
    margin-left: 0%;
    width: 100%;
  }
}

</style>