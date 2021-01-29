<template>
    <div class="experience">
        <div class="shadow"></div>
        <div class="header">
            <h2>{{ title }}</h2>
        </div>
        <div class="list-one-title">
            <h3>{{ info.firstTitle }}</h3>
        </div>
        <ul class="list-one">
            <li v-for="(item, index) in list(info.firstList)" :key="index">
                {{ item.endsWith('.') ? item : `${item};` }}
            </li>
        </ul>
        <div class="list-two-title">
            <h3>{{ info.secondTitle }}</h3>
        </div>
        <ul class="list-two">
            <li v-for="(item, index) in list(info.secondList)" :key="index">
                {{ item.endsWith('.') ? item : `${item};` }}
            </li>
        </ul>
    </div>    
</template>

<script>
export default {
    props: [
        'title',
        'info'
    ],
    methods: {
        list(item) {
            if(item)
            return item.split(';');
        }
    }
}
</script>