<template>
    <div ref="project" class="project">
        <Gallery v-if="isGalleryActive" 
            :image="currentImage" 
            :gallery="currentGallery" 
            @change-image="changeImage"
            @close-gallery="closeGallery"
        />
        <div class="image" :style="`background-image: url(${require(`../assets/img/projects/${project.path}.jpg`)})`"></div>
        <div :class="isMore ? 'info show' : 'info'">
            <h3>{{ project.name }}</h3>
            <div v-if="isMore" class="more">
                <div>
                    <p>Short info:</p>
                    <p>{{ project.info[lang] }}</p>
                </div>
                <div>
                    <p>Technology:</p>
                    <div>
                        <img v-for="(image, index) in project.icons" 
                            :key="index" 
                            :src="require(`../assets/img/icons/${image}.png`)" 
                            :alt="project.name"
                        >
                    </div>
                </div>
                <div>
                    <p>More images:</p>
                    <div>
                        <img v-for="(image, index) in project.images" 
                            :key="index" 
                            :src="require(`../assets/img/projects/images/${image}`)" 
                            :alt="project.name"
                            @click="selectImage(image)"
                        >
                    </div>
                </div>
            </div>
            <div v-else>
                <a :href="`https://github.com/TM85dev/${project.github}`" class="github" target="_blank">GitHub</a>
                <a :href="`http://tm-dev.pl/${project.live}`" class="github" target="_blank">Life</a>
            </div>
            <div @click="toggleInfo">{{ isMore ? less[lang] : more[lang] }}</div>
        </div>
    </div>
</template>

<script>
export default {
    props: [
        'project', 'lang'
    ],
    data: () => ({
        isMore: false,
        isGalleryActive: false,
        more: { uk: 'More', pl: 'Więcej' },
        less: { uk: 'Less', pl: 'Mniej' },
        currentImage: '',
        currentGallery: ''
    }),
    methods: {
        toggleInfo() {
            this.isMore = !this.isMore;
        },
        selectImage(image) {
            this.currentImage = image;
            this.currentGallery = this.project.images;
            this.isGalleryActive = true;
            this.$refs.project.style.transform = 'none';
        },
        changeImage(image) {
            this.currentImage = image;
        },
        closeGallery() {
            this.isGalleryActive = false;
            this.$refs.project.style.transform = '';
        },
    },
}
</script>