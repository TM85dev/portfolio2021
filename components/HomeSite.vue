<template>
    <div ref="site" class="home-site" @mousemove="mouseMoveHandler">
        <!-- <ParallaxBg ref="parallax" /> -->
        <div ref="logo" id="logo">
            <div class="logo"></div>
            <div class="greetings">
                <h1>WELCOME</h1>
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
            <p>SCROLL DOWN</p>
            <div></div>
        </div>
    </div>
</template>

<script>
export default {
    computed: {
        greetings() {
            return 'TO MY WEBSITE'.split('');
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