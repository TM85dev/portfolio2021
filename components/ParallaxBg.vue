<template>
    <div 
        ref="parallax" 
        class="bg-parallax">
    </div>
</template>

<script>
export default {
    mounted() {
        const el = this.$refs.parallax;
        document.body.addEventListener('mousemove', (e) => {
            el.style.backgroundPosition = `${e.pageX / 15}px ${e.pageY / 15}px`;
        })
    }
}
</script>