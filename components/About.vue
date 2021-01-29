<template>
    <div class="about-site">
        <AboutMe :title="titleAboutMe[lang]" :info="infoAboutMe[lang]" />
        <Experience :title="titleExperience[lang]" :info="infoExperience[lang]" />
        <Hobby :info="infoHobby[lang]" />
    </div>
</template>

<script>
export default {
    props: ['lang'],
    data: () => ({
        data: [],
        titleAboutMe: {uk: "About Me", pl: "O Mnie"},
        titleExperience: {uk: "Experience", pl: "Doświadczenie"},
        infoAboutMe: {uk: [], pl: []},
        infoExperience: {uk: [], pl: []},
        infoHobby: {uk: [], pl: []}
    }),
    mounted() {
        this.$axios.$get('/api/about/')
            .then(res => {
                res.forEach(item => {
                    this.data = {
                        ...this.data,
                        [item.name]: item.value
                    }
                })
                this.infoAboutMe = {
                    uk: this.data.info_learning_uk,
                    pl: this.data.info_learning_pl
                }
                this.infoExperience = {
                    uk: {
                        firstTitle: this.data.first_title_uk,
                        firstList: this.data.first_list_uk,
                        secondTitle: this.data.second_title_uk,
                        secondList: this.data.second_list_uk
                    },
                    pl: {
                        firstTitle: this.data.first_title_pl,
                        firstList: this.data.first_list_pl,
                        secondTitle: this.data.second_title_pl,
                        secondList: this.data.second_list_pl
                    }
                }
                this.infoHobby = {
                    uk: this.data.hobby_uk,
                    pl: this.data.hobby_pl
                }
            })
    },
    methods: {
        // condition(item) {
        //     return this.lang==='uk' ? item.uk : item.pl;
        // }
    },
}
</script>