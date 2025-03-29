<script setup lang="ts">
  import { ref } from 'vue';
  import { UseElementVisibility } from '@vueuse/components'
  import Header from './components/Navigation.vue'
  import Works from './components/Works.vue'


    const infos = {
        name: 'MAXIME CUCHE',
        metier: 'Développeur web',
        identité: 'Maxime Cuche',
        propos: `Je suis un développeur web passionné
        par la création de sites internet et de maquettes graphiques 
        basé à Mercuès dans le LOT.`,
        email: 'maxcuche@gmail.com',
        footer: '© 2021 - Tous droits réservés',
        liens: [
            { nom: 'Acceuil', url: '#' },
            { nom: 'Réalisations', url: '#' },
            { nom: 'Contact', url: '#' },
            { nom: 'Réseaux', url: '#' },
        ]
    }

    const presentation = ref(
        `Depuis toujours, je suis passionné par l'informatique et l'IA que je découvre à travers diverses expériences en autodidact. Depuis peu, j’ai le projet d’orienter ma carrière en tant que développer web.
        En effet, depuis l’époque de ma carrière de paysagiste, j’ai toujours eu le goût du travail d'équipe. Que ce soit lors des travaux pratiques ou lors des projets auquel j'ai participé, j’avais déjà apprécié le fait de pouvoir assouvir ma curiositée ainsi que l’exigence de la qualitée qui m’animait.
        A la suite de ma reconversion professionnel, j’ai logiquement choisi de suivre une formation de développeur web en accord avec ma passion de la programmation, de l’outil informatique et de l'élaboration de maquettes graphiques.
        Cette formation a complètement et totalement confirmé que je voulais poursuivre dans cette voie. Je suis déterminé et conscient que ce métier est en perpétuel évolution. Je suis sur qu'il correspond parfaitement à mes qualitées.
        Je possède des compétences techniques solides et je maitrise les langages HTML, CSS, JavaScript, ainsi que des frameworks comme Vue.js. Je suis quelqu'un de créatif capable de concevoir des interfaces utilisateur attrayantes et intuitives
        Je sait résoudre des problèmes parfois complex pour identifier et corriger les bugs rapidement et efficacement. J'aime apprendre continuelement car le domaine du développement web évolue constamment, donc rester à jour avec les dernières technologies et tendances est vital.
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

</script>






<template>
    <Header :name="infos.name" :metier="infos.metier" :liens="infos.liens" />
  
    <main :style="{ backgroundColor: '#fffeef', color: '#f20e0e',  }">
        <section :style="{ display: 'flex', flexDirection: 'column', alignItems: 'center', textTransform: 'uppercase', textAlign: 'center' }">    
            <h1 :style="{ paddingTop: '250px', paddingBottom: '80px', marginBottom:'0px', fontSize: '250px', lineHeight: '300px', fontWeight: 'lighter', letterSpacing: '-7.5px' }">{{ infos.identité }}</h1>
            <p :style="{ fontSize:'27px', lineHeight:'30px', fontWeight: '400px', letterSpacing:'-2px', whiteSpace: 'pre-wrap', paddingBottom: '120px', margin: '0px' }">{{ infos.propos }}</p>
            <a :href="'mailto:' + infos.email" :style="{ color: '#f20e0e', fontSize: '24px', fontWeight: '500px', lineHeight: '24px', paddingBottom: '190px' }">{{ infos.email }}</a>
        </section>
        <UseElementVisibility v-slot="{ isVisible }">
            <section :class="{ slide: isVisible }" :style="{ fontWeight: '400px', fontSize: '21px', paddingLeft: '250px', paddingRight: '250px', textShadow: '1px 1px 2px #473030' }">
                <article>
                    <p :style="{ lineHeight: '24px', whiteSpace: 'pre-wrap' }">{{ presentation }}</p>
                </article>
            </section>
        </UseElementVisibility>
        <Works :card="travaux.card" :ls="travaux.ls" :NFT="travaux.NFT" :art="travaux.art" :gaming="travaux.gaming" :troisD="travaux.troisD" />
    </main>
    
</template>






<style scoped>

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