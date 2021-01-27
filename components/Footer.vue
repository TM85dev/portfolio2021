<template>
    <footer>
        <div class="shadow"></div>
        <div class="title">
            <div :style="`background-image: url(${logo})`"></div>
            <p>My Portfolio</p>
        </div>
        <div class="icons">
            <div 
                v-for="(icon, index) in icons" :key="index"
                :class="(index===3 && !isTopButtonActive) ? 'active' : ''"
                @click="clickHandler(icon.name)">
                <span :style="`background-image: url(${icon.path})`"></span>
            </div>
        </div>
        <p class="copyright">© 2021. All rights reserved by Tomasz Mączka</p>
    </footer>
</template>

<script>
export default {
    props: [
        'isTopButtonActive'
    ],
    data() {
        return {
            logo: require('../assets/img/logo.png'),
            icons: [
                {name: 'email', path: require('../assets/img/mail.svg')},
                {name: 'linkedin', path: require('../assets/img/linkedin.svg')},
                {name: 'github', path: require('../assets/img/github.svg')},
                {name: 'top', path: require('../assets/img/arrow.png')}
            ]
        }
    },
    methods: {
        clickHandler(name) {
            if(name==='email') {
                const contact = document.querySelector('.contact-site');
                const contactForm = contact.querySelector('form label:first-of-type input');
                contact.scrollIntoView({ behavior: 'smooth' });
                setTimeout(() => contactForm.focus(), 400);
            }
        }
    }
}
</script>