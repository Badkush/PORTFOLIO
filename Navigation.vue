<template>
    <header :style="{ backgroundColor: 'transparent', color: '#f20e0e', fontSize: '23px', lineHeight: '23px', fontWeight: 'bold', letterSpacing: '-1.5px', position: 'fixed', top: '0px', width: '100%', backdropFilter: 'blur(10px)' }">
        <nav :style="{ paddingTop: '70px', display: 'flex', justifyContent: 'space-between', alignItems: 'center' }">
            <section :style="{ display: 'flex', flexDirection: 'column', paddingLeft: '65px'}">
                <a href="#">                    
                    <p>{{ name }} <br>
                    <span :style="{ fontWeight: 'normal', lineHeight: '19px' }">{{ metier }}</span>
                    </p>
                </a>
            </section>
            <section>
                <ul :style="{ display: 'flex', listStyle: 'none', gap: '50px', textTransform: 'uppercase', textDecoration: 'none', paddingRight: '65px' }">
                    <li v-for="lien in liens" :key="lien.nom">
                        <a :href="lien.url">{{ lien.nom }}</a>
                    </li>
                </ul>
            </section>
        </nav>
    </header>
</template>

<script setup lang="ts">

// je vais utiliser le defineProps pour définir les props que je vais passer au composant Header
defineProps<{
    name: string,
    metier: string,
    liens: { nom: string, url: string }[]
}>();
</script>

<style scoped>
nav a {
    text-decoration: none;
    color: #f20e0e;
}

a:hover {
    text-decoration: underline;
}
</style>
