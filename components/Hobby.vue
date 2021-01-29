<template>
    <div class="hobby">
        <div class="shadow"></div>
        <div class="info">
            <div>
                <p>{{ info }}</p>
            </div>
            <div></div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['info']
}
</script>