<template>
    <div @click.self="closeGallery" ref="gallery" class="gallery">
        <span @click="closeGallery" class="close"></span>
        <img :src="require(`../assets/img/projects/images/${image}`)" :alt="name(image)">
        <div>
            <img v-for="(pic, index) in gallery" 
                :key="index" 
                :src="require(`../assets/img/projects/images/${pic}`)" 
                :alt="name(pic)"
                @click="changeImage(pic)"
            >
        </div>
    </div>
</template>

<script>
export default {
    props: ['image', 'gallery'],
    methods: {
        name(name) {
            return name.slice(0, name.length - 4);
        },
        changeImage(pic) {
            this.$emit('change-image', pic);
        },
        closeGallery() {
            this.$anime({
                targets: this.$refs.gallery,
                opacity: 0,
                scale: 0,
                easing: 'easeOutExpo',
                complete: () => this.$emit('close-gallery')
            })
        }
    }
}
</script>