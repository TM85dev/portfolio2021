<template>
    <div class="aboutme-site">
        <div class="shadow"></div>
        <div class="header">
            <h2>{{ title }}</h2>
        </div>
        <div class="info-learning">
            <div>
                <p v-for="(text, index) in infoLearning" :key="index">{{ text }}</p>
            </div>
            <div></div>
        </div>
    </div>
</template>

<script>
export default {
    props: [
        'title',
        'info'
    ],
    computed: {
        infoLearning() {
            if(String(this.info))
            return this.info.split('\r\n');
        }
    }
}
</script>