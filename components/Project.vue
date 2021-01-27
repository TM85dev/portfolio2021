<template>
    <div class="project">
        <div class="image" :style="`background-image: url(${require(`../assets/img/projects/${project.path}.jpg`)})`"></div>
        <div class="info">
            <h3>{{ project.name }}</h3>
            <div>
                <a href="" class="github">GitHub</a>
                <a href="" class="github">Life</a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: [
        'project'
    ]
}
</script>