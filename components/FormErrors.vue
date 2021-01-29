<template>
    <div ref="errors" class="errors">
        <div class="close" @click="closeErrors"></div>
        <p v-if="errors.name[lang]">* {{ errors.name[lang] }}</p>
        <p v-if="errors.email[lang]">* {{ errors.email[lang] }}</p>
        <p v-if="errors.message[lang]">* {{ errors.message[lang] }}</p>
    </div>
</template>

<script>
export default {
    props: [
        'lang',
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