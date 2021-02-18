<template>
    <div class="projects-site">
        <div class="shadow"></div>
        <div class="header">
            <h2>{{ title[lang] }}</h2>
        </div>
        <div class="projects-list">
            <Project v-for="(project, index) in projects" :key="index" :project="project" />
        </div>
    </div>
</template>

<script>
export default {
    props: ['lang'],
    data: () => ({
        title: {uk: 'My Projects', pl: 'Moje Projekty'},
        projects: [
            {name: 'Agency Site', path: 'agency_site'},
            {name: 'Dogs Site', path: 'dogs_site'},
            {name: 'Faktura Creator', path: 'faktura'},
            {name: 'Pairs Game', path: 'pairs_game'},
            {name: 'Portfolio 2020', path: 'portfolio'},
            {name: 'Rock Paper Sicisors', path: 'rock_paper_sicisors'},
            {name: 'Todo Manager', path: 'todo'},
        ]
    }),
}
</script>