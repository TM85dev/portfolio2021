<template>
    <div ref="skill" class="skill" @click="clickHandler">
        <div class="icon" 
            :style="`background-image: url(${require(`../assets/img/icons/${skill}.png`)})`"
        ></div>
    </div>
</template>

<script>
export default {
    props: [
        'skill',
    ],
    mounted() {
        (this.skill==='html' || this.skill==='php' || this.skill==='git') ? this.clickHandler() : null;
    },
    methods: {
        clickHandler() {
            const skills  = document.querySelectorAll('.skills-site .skills-icons .skill');
            skills.forEach(skill => skill.classList.remove('active'));
            this.$refs.skill.classList.add('active');
            this.$emit('is-loading', true);
            this.$axios.$get(`/api/skills/${this.skill}`)
            .then(res => {
                this.$emit('current-skill', res);
            }).finally(() => {
                this.$emit('is-loading', false);
            }).catch(e => {})
        }
    }
}
</script>