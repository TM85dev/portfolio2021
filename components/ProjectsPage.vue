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
            {
                name: 'Agency Site', 
                path: 'agency_site', 
                github: 'site-project', 
                live: 'agency-site',
                info: {
                    uk: 'Website project for an advertising company.\nMainly based on the Vue framework.\nResponsive page. Date loaded from json files.\nAdditionally used: vue-router, vue-lazyload.',
                    pl: 'Projekt strony internetowej dla agencji reklamowej.\nGłównie oparty na frameworku Vue.\nStrona responsywna. Data ładowana z plików json.\nDodatkowo wykorzystano: vue-router, vue-lazyload.',
                },
                icons: ['vue', 'scss', 'bootstrap', 'animejs'],
                images: ['agency_site_1.jpg', 'agency_site_2.jpg', 'agency_site_3.jpg'],
            },
            {
                name: 'Dogs Site', 
                path: 'dogs_site', 
                github: 'dog-training', 
                live: 'tresura',
                info: {
                    uk: 'Dog trainer website project.\nMainly based on React framework.\nResponsive website.\nAdditionally used: react hooks, react-router-dom, react-spring.',
                    pl: 'Projekt strony internetowej tresera psów.\nGłównie oparty na frameworku React.\nStrona responsywna.\nDodatkowo wykorzystano: react hooks, react-router-dom, react-spring.',
                },
                icons: ['react', 'scss'],
                images: ['dog_site_1.jpg', 'dog_site_2.jpg', 'dog_site_3.jpg'],
            },
            {
                name: 'Movies Site', 
                path: 'movies_list', 
                github: 'movies-list', 
                live: 'movies-list',
                info: {
                    uk: 'Website project for movie lists.\nFront-end based on Vue. Back-end - Laravel.\nResponsive page.\nAdditionally used: Vuex.',
                    pl: 'Projekt strony internetowej listy filmów.\nFront-end oparty na Vue. Back-end - Laravel.\nStrona responsywna.\nDodatkowo wykorzystano: Vuex.',
                },
                icons: ['vue', 'scss', 'axios', 'animejs', 'laravel'],
                images: ['movies_site_1.jpg', 'movies_site_2.jpg', 'movies_site_3.jpg'],
            },
            {
                name: 'Faktura Creator', 
                path: 'faktura', 
                github: 'faktura-generator', 
                live: 'faktura',
                info: {
                    uk: 'Facture generator project for pdf file.\nMainly based on the React framework.\nResponse page.\nAdditionally used: react hooks, react-router-dom, react-spring, react-redux, react-pdf.',
                    pl: 'Projekt generatora faktury do pliku pdf.\nGłównie oparty na frameworku React.\nStrona responsywna.\nDodatkowo wykorzystano: react hooks, react-router-dom, react-spring, react-redux, react-pdf.',
                },
                icons: ['react', 'redux', 'scss'],
                images: ['faktura_creator_1.jpg', 'faktura_creator_2.jpg', 'faktura_creator_3.jpg'],
            },
            {
                name: 'Pairs Game', 
                path: 'pairs_game', 
                github: 'pairs', 
                live: 'pairs',
                info: {
                    uk: 'Pairs game project.\nDrawing two of the same cards to score points.\nJQuery-based mechanics.\nAdditionally used: jQuery-transit.',
                    pl: 'Projekt gry w pary.\nDobieranie dwóch takich samych kart, aby zdobyć punkty.\nMechanika oparta na jQuery.\nDodatkowo wykorzystano: jQuery-transit.',
                },
                icons: ['html', 'bootstrap', 'jquery', 'scss'],
                images: ['pairs_game_1.jpg', 'pairs_game_2.jpg', 'pairs_game_3.jpg'],
            },
            {
                name: 'Portfolio 2020', 
                path: 'portfolio', 
                github: 'portfolio', 
                live: 'portfolio',
                info: {
                    uk: 'Portfolio website project.\nMainly based on React.\nApi framework for sending e-mails created with Express.\nAdditionally used: react hooks, react-router-dom, react-spring, react-recaptcha, nodemailer.',
                    pl: 'Projekt strony internetowej typu portfolio.\nGłównie oparty na frameworku React.\nApi do wysyłania e-maila stworzone za pomocą Express’a.\nDodatkowo wykorzystano: react hooks, react-router-dom, react-spring, react-recaptcha, nodemailer.',
                },
                icons: ['react', 'express', 'axios', 'scss'],
                images: ['portfolio_2020_1.jpg', 'portfolio_2020_2.jpg', 'portfolio_2020_3.jpg'],
            },
            {
                name: 'Rock Paper Sicisors', 
                path: 'rock_paper_sicisors', 
                github: 'rock-paper-sicisors', 
                live: 'rps',
                info: {
                    uk: 'Project of the popular game rock-paper-scissors.\nAfter scoring/losing 1,000 points, the game is over.\nMechanics based on jQuery.\nAdditionally used: jQuery-transit.',
                    pl: 'Projekt popularnej gry papier-kamień-nożyce.\nPo zdobyciu/straceniu 1 000 punktów gra się kończy.\nMechanika oparta na jQuery.\nDodatkowo wykorzystano: jQuery-transit.',
                },
                icons: ['html', 'bootstrap', 'jquery', 'scss'],
                images: ['rps_1.jpg', 'rps_2.jpg', 'rps_3.jpg'],
            },
            {
                name: 'Todo Manager', 
                path: 'todo', 
                github: '', 
                live: 'todo/public/',
                info: {
                    uk: 'To-do list manager website project.\nFront-end based on Vue. Back-end - Laravel.\nResponsive page.\nAdditionally used: vue-animejs.',
                    pl: 'Projekt strony internetowej manadżera listy zadań.\nFront-end oparty na Vue. Back-end - Laravel.\nStrona responsywna.\nDodatkowo wykorzystano: vue-animejs.',
                },
                icons: ['vue', 'jquery', 'bootstrap', 'scss', 'axios', 'laravel'],
                images: ['todo_manager_1.jpg', 'todo_manager_2.jpg', 'todo_manager_3.jpg'],
            },
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
}
</script>