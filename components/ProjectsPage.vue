<template>
    <div class="projects-site">
        <div class="shadow"></div>
        <div class="header">
            <h2>My Projects</h2>
        </div>
        <Project v-for="(project, index) in projects" :key="index" :project="project" />
    </div>
</template>

<script>
export default {
    data() {
        return {
            projects: [
                {name: 'Agency Site', path: 'agency_site'},
                {name: 'Dogs Site', path: 'dogs_site'},
                {name: 'Faktura Creator', path: 'faktura'},
                {name: 'Pairs Game', path: 'pairs_game'},
                {name: 'Portfolio 2020', path: 'portfolio'},
                {name: 'Rock Paper Sicisors', path: 'rock_paper_sicisors'},
                {name: 'Todo Manager', path: 'todo'},
            ]
        }
    },
}
</script>