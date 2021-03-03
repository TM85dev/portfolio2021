<template>
    <div class="projects-site">
        <div class="shadow"></div>
        <div class="header">
            <h2>{{ title[lang] }}</h2>
        </div>
        <div class="projects-list">
            <Project v-for="(project, index) in projects" :key="index" :project="project" :lang="lang" />
        </div>
    </div>
</template>

<script>
export default {
    props: ['lang'],
    data: () => ({
        title: {uk: 'My Projects', pl: 'Moje Projekty'},
        projects: [
            // {
            //     name: 'Portfolio 2021', 
            //     path: 'portfolio_2021', 
            //     github: 'portfolio_2021', 
            //     live: '/',
            //     info: {
            //         uk: 'Portfolio website project.\nFront-end based on Nuxt(Vue). Back-end - PHP.\nResponsive page.\nAdditionally used: cookie-universal-nuxt, nuxt-animejs.',
            //         pl: 'Projekt strony internetowej portfolio.\nFront-end oparty na Nuxt(Vue). Back-end - PHP.\nStrona responsywna.\nDodatkowo wykorzystano: cookie-universal-nuxt, nuxt-animejs.',
            //     },
            //     icons: ['nuxtjs', 'axios', 'animejs', 'scss', 'php'],
            //     images: ['portfolio_2021_1.jpg', 'portfolio_2021_2.jpg', 'portfolio_2021_3.jpg'],
            // },
        ]
    }),
    mounted() {
        this.$axios.$get('/api/projects/')
            .then(res => {
                res.map(project => {
                    this.projects = this.projects.concat({
                        ...project,
                        info: {
                            uk: project.infoUK.replaceAll('\\n', ''),
                            pl: project.infoPL.replaceAll('\\n', '')
                        },
                        icons: project.icons.split(',').map(icon => icon.trim()),
                        images: project.images.split(',').map(image => image.trim())
                    })
                })
            }).catch(e => {})
    }
}
</script>