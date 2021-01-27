<template>
    <div ref="top" class="to-top" @click="toTopHandler">
        <div></div>
    </div>
</template>

<script>
export default {
    props: [
        'isTopButtonActive'
    ],
    watch: {
        isTopButtonActive() {
            this.$anime({
                targets: this.$refs.top,
                scale: this.isTopButtonActive ? [0, 1] : [1, 0],
                easing: 'easeOutExpo',
                duration: 600,
                begin: () => {
                    this.$refs.top.style.display =  'block';
                },
                complete: () => {
                    this.$refs.top.style.display = this.isTopButtonActive ? 'block' : 'none';
                }
            })
        }
    },
    methods: {
        toTopHandler() {
            window.scrollTo({top: 0, left: 0, behavior: 'smooth'});
        }
    }
}
</script>