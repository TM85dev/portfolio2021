<template>
    <div ref="bg" class="bg-overlay-menu" @click.self="closeMobileMenu">
        <div ref="overlayMenu" class="overlay-menu">
            <div ref="close" class="close" @click="closeMobileMenu">
                <svg viewBox="0 0 200 200">
                    <path 
                        d="
                            M 100, 100
                            m -75, 0
                            a 75,75 0 1,0 150,0
                            a 75,75 0 1,0 -150,0
                            "
                    />
                </svg>
                <div></div>
            </div>
            <div ref="logo" class="logo"></div>
            <ul ref="list" class="overlay-menu-list">
                <li v-for="(link, index) in list" :key="index">
                    <a :href="`/${link.name}`" 
                        @click.prevent="scrollHandler(link.name.uk)">
                            {{ link.name[lang] }}
                    </a>
                    <div></div>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    props: ['lang'],
    data: () => ({
        list: [
            {name: { uk: 'Home', pl: 'Strona Główna' }},
            {name: { uk:'Skills', pl: 'Umiejętności' }},
            {name: { uk:'Projects', pl: 'Projekty' }},
            {name: { uk:'About Me', pl: 'O Mnie' }},
            {name: { uk:'Contact', pl: 'Kontakt' }},
        ]
    }),
    mounted() {
        const elDOM = el => document.querySelector(el);
        const sites = [elDOM('.home-site'), elDOM('.skills-site'), elDOM('.projects-site'), elDOM('.about-site'), elDOM('.contact-site')];
        sites.forEach((ref, index) => {
            const rect = ref.getBoundingClientRect();
            const link = document.querySelector(`.overlay-menu-list li:nth-of-type(${index + 1})`);
            const menuHeight = elDOM('nav').getBoundingClientRect().height;
            if(rect.top <= menuHeight && rect.bottom >= menuHeight) {
                link.classList.add('active');
            } else {
                link.classList.remove('active');
            }
        });
        this.$anime.timeline({
            targets: this.$refs.overlayMenu,
            width: ['0%', '100%'],
            easing: 'easeInOutExpo'
        }).add({
            targets: this.$refs.logo,
            scale: [0, 1],
            opacity: [0, 1],
            easing: 'easeOutExpo',
            delay: 400,
            duration: 600
        }).add({
            targets: this.$refs.list.children,
            translateY: [-20, 0],
            opacity: [0, 1],
            delay: this.$anime.stagger(100),
            easing: 'easeOutExpo',
            duration: 600
        })
        this.$anime({
            targets: this.$refs.close,
            opacity: [0, 1],
            easing: 'easeOutExpo',
            delay: 800
        })
    },
    methods: {
        closeMobileMenu() {
            this.$anime({
                targets: this.$refs.list.children,
                translateY: [0, -20],
                opacity: [1, 0],
                delay: this.$anime.stagger(100, {direction: 'reverse'}),
                easing: 'easeOutExpo',
                duration: 600
            });
            this.$anime({
                targets: [this.$refs.close, this.$refs.logo],
                opacity: [1, 0],
                easing: 'easeOutExpo',
                duration: 600
            })
            this.$anime({
                targets: this.$refs.overlayMenu,
                width: ['100%', '0%'],
                easing: 'easeInOutExpo',
                complete: () => {
                    this.$emit('close-mobile-menu');
                }
            })
        },
        scrollHandler(name) {
            const el = name.replace(' ', '').toLowerCase();
            document.querySelector(`.${el}-site`).scrollIntoView({behavior: 'smooth'});
            this.closeMobileMenu();
            if(name.toLowerCase()==='contact') {
                const elDOM = e => document.querySelector(e);
                const contact = elDOM('.contact-site').getBoundingClientRect(); 
                setTimeout(() => elDOM('.contact-site form label:first-of-type input').focus(), contact.top > 500 ? 1000 : 400);
            }
        }
    }
}
</script>