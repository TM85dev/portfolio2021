<template>
    <footer>
        <div class="shadow"></div>
        <div class="title">
            <div :style="`background-image: url(${logo})`"></div>
            <p>{{ title[lang] }}</p>
        </div>
        <div class="icons">
            <div 
                v-for="(icon, index) in icons" :key="index"
                :class="(index===3 && !isTopButtonActive) ? 'active' : ''"
                @click="clickHandler(icon.name, icon.link)">
                <span :style="`background-image: url(${icon.path})`"></span>
            </div>
        </div>
        <p class="copyright">© 2021. {{ copyrights[lang] }}</p>
    </footer>
</template>

<script>
export default {
    props: [
        'isTopButtonActive',
        'lang'
    ],
    data: () => ({
        title: {uk: 'My Portfolio', pl: 'Moje Portfolio'},
        copyrights: { uk: ' All rights reserved.', pl: ' Wszelkie prawa zastrzeżone.' },
        logo: require('../assets/img/logo.png'),
        icons: [
            {name: 'email', path: require('../assets/img/mail.svg')},
            {name: 'linkedin', path: require('../assets/img/linkedin.svg'), link: 'linkedin.com/in/tmdev85'},
            {name: 'github', path: require('../assets/img/github.svg'), link: 'github.com/TM85dev'},
            {name: 'top', path: require('../assets/img/arrow.png')}
        ]
    }),
    methods: {
        clickHandler(name, link) {
            if(name==='email') {
                const contact = document.querySelector('.contact-site');
                const contactForm = contact.querySelector('form label:first-of-type input');
                contact.scrollIntoView({ behavior: 'smooth' });
                setTimeout(() => contactForm.focus(), 400);
            } else if(name==='top') {
                window.scroll({top: 0, left: 0, behavior: 'smooth'});
            } else {
                window.open(`https://${link}`, '_blank');
            }
        }
    }
}
</script>