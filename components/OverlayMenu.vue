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
                    <a :href="`/${link.name[lang]}`" 
                        @click.prevent="clickToScrollOverlay(link.name.uk)">
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
    props: [
        'lang',
        'list',
        'currentLinkActive',
        'clickToScroll'
    ],
    mounted() {
        this.currentLinkActive('.overlay-menu-list li');
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
        clickToScrollOverlay(name) {
            this.closeMobileMenu();
            this.clickToScroll(name);
        },
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
    }
}
</script>