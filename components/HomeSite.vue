<template>
    <div ref="site" class="home-site" @mousemove="mouseMoveHandler">
        <div ref="logo" id="logo">
            <div class="logo"></div>
            <div class="greetings">
                <h1>{{ lang==='uk' ? header.uk : header.pl }}</h1>
                <p ref="letters"><span 
                    v-for="(letter, index) in greetings" :key="index"
                    v-anime="{
                        translateX: [-6, 0],
                        opacity: [0, 1],
                        scale: [0, 1],
                        delay: 600 + (index * 70),
                        duration: 600,
                        easing: 'easeOutExpo'
                }">{{ letter }}
                </span></p>
            </div>
        </div>
        <div class="scroll-down" @click="scrollDown">
            <p>{{ lang==='uk' ? scrollInfo.uk : scrollInfo.pl }}</p>
            <div></div>
        </div>
    </div>
</template>

<script>
export default {
    props: [
        'lang'
    ],
    data: () => ({
        header: {uk: 'WELCOME', pl: 'WITAJ'},
        underHeader:  {uk: 'TO MY WEBSITE', pl: 'NA MOJEJ STRONIE'},
        scrollInfo: {uk: 'SCROLL DOWN', pl: 'PRZEWIŃ W DÓŁ'}
    }),
    computed: {
        greetings() {
            return this.lang==='uk' ? this.underHeader.uk.split('') : this.underHeader.pl.split('');
        }
    },
    methods: {
        mouseMoveHandler(e) {
            this.$refs.logo.style.margin = `${e.pageY * -1 / 20}px ${e.pageX * -1 / 20}px`;
        },
        scrollDown() {
            const mySkills = document.querySelector('.skills-site');
            mySkills.scrollIntoView({ behavior: 'smooth' });
        }
    }
}
</script>