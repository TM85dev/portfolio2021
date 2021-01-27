<template>
    <div ref="errors" class="errors">
        <div class="close" @click="closeErrors"></div>
        <p v-if="errors.name">* {{ errors.name }}</p>
        <p v-if="errors.email">* {{ errors.email }}</p>
        <p v-if="errors.message">* {{ errors.message }}</p>
    </div>
</template>

<script>
export default {
    props: [
        'inputs',
        'errors'
    ],
    mounted() {
        this.$anime({
            targets: this.$refs.errors,
            translateX: ['-100%', '0%'],
            easing: 'easeOutExpo',
        })
    },
    beforeDestroy() {

    },
    methods: {
        closeErrors() {
            this.$anime({
                targets: this.$refs.errors,
                translateX: ['0%', '-100%'],
                easing: 'easeOutExpo',
                complete: () => {
                    this.$emit('close-errors');
                }
            })
        }
    }
}
</script>