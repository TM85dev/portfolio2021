<template>
    <div v-if="isNotAccepted" class="cookies">
        <p>{{ info[lang] }}</p>
        <button @click="acceptCookies">OK</button>
    </div>
</template>

<script>
export default {
    props: ['lang'],
    data: () => ({
        info: {
            uk: 'This site uses cookies',
            pl:' Ta strona używa ciasteczek'
        },
        isNotAccepted: false
    }),
    beforeMount() {
        if(!this.$cookies.get('accepted')) {
            this.$cookies.set('accepted', 'false', { path: '/', maxAge: 60*60*24 });
            this.isNotAccepted = true;
        } else {
            if(this.$cookies.get('accepted') === 'true') {
                this.isNotAccepted = false;
            } else if(this.$cookies.get('accepted') === 'false') {
                this.isNotAccepted = true;
            }
        }
    },
    methods: {
        acceptCookies() {
            this.$cookies.set('accepted', 'true', { path: '/', maxAge: 60*60*24*7 });
            this.isNotAccepted = false
        }
    }
}
</script>