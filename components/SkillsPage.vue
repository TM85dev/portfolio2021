<template>
    <div class="skills-site">
        <div class="shadow"></div>
        <div class="header">
            <h2>{{ lang==='uk' ? title.uk : title.pl }}</h2>
        </div>
        <div class="skills-menu">
            <div :ref="select.ref" :class="select.isActive ? 'select visible active' : 'select visible'" 
                v-for="select in skillsMenu" :key="select.id" 
                @mouseenter.self="selectHoverHandler(select)" 
                @mouseleave.self="selectLeaveHandler(select)"
            >
                <div @click.self="selectClickHandler(select)">
                    {{ lang==='pl' && select.id===3 ? 'Inne' : select.name }}
                </div>
                <div></div>
            </div>
        </div>
        <template v-for="(skillMenu, i) in skillsMenu">
        <div v-if="skillMenu.isActive" class="skills-icons" :key="i">
            <SkillIcon v-for="(skill, index) in currentSkillsIcons(skillMenu.name)" :key="index" :skill="skill" @current-skill="currentSkill" @is-loading="loadingHandler" />
        </div>
        </template>
        <div ref="skillInfo" class="skill-info">
            <img v-if="isLoading" src="../assets/img/loader.svg" alt="loader">
            <template v-else>
                <div class="icon">
                    <div :style="`background-image: url(${require(`../assets/img/icons/${skillInfo.name}.png`)})`"></div>
                </div>
                <p>
                    <span>{{ skillInfo.title }}</span>
                    <span>{{ lang==='uk' ? skillInfo.descriptionUK : skillInfo.descriptionPL }}</span>
                </p>
            </template>
        </div>
    </div>
</template>

<script>
export default {
    props: ['lang'],
    data: () => ({
        title: {uk: 'My Skills', pl: 'Moje Umiejętności'},
        isLoading: false,
        skillInfo: {name: 'html'},
        skillsMenu: [
            {id: 1, name: 'Front-End', isActive: true, ref: 'frontend'},
            {id: 2, name: 'Back-End', isActive: false, ref: 'backend'},
            {id: 3, name: 'Other', isActive: false, ref: 'other'},
        ],
        frontEndSkills: [
            'html', 'css', 'scss', 'animejs', 'bootstrap', 'js', 'jquery', 'react', 'nextjs', 'vue', 'nuxtjs'
        ],
        backEndSkills: [
            'php', 'laravel', 'nodejs', 'express', 'mariadb', 'mongodb'
        ],
        otherSkills: [
            'git', 'github', 'linux', 'npm', 'axios', 'wordpress', 'responsive', 'mobile_first', 'rest_api'
        ]
    }),
    methods: {
        currentSkillsIcons(name) {
            return name==='Front-End' ? this.frontEndSkills : (name==='Back-End' ? this.backEndSkills : this.otherSkills);
        },
        loadingHandler(toggle) {
            this.isLoading = toggle;
        },
        currentSkill(data) {
            this.skillInfo = data;
            this.$anime({
                targets: this.$refs.skillInfo,
                opacity: [0, 1],
                easing: 'easeOutExpo'
            });
        },
        mouseMoveHandler(e) {
            this.$refs.parallax.$el.style.backgroundPosition = `${e.pageX / 15}px ${e.pageY / 15}px`;
        },
        selectHoverHandler(select) {
            if(!select.isActive) {
                this.$anime({
                    targets: this.$refs[select.ref][0].children[0],
                    color: '#ea474d',
                    easing: 'easeOutExpo'
                });
                this.$anime({
                    targets: this.$refs[select.ref][0].children[1],
                    width: ['30%', '80%'],
                    backgroundColor: '#ea474d',
                    easing: 'easeOutExpo'
                });
            }
        },
        selectLeaveHandler(select) {
            if(!select.isActive) {
                this.$anime({
                    targets: this.$refs[select.ref][0].children[0],
                    color: 'rgb(211 211 211)',
                    easing: 'easeOutExpo'
                });
                this.$anime({
                    targets: this.$refs[select.ref][0].children[1],
                    width: ['80%', '30%'],
                    backgroundColor: 'rgb(211 211 211)',
                    easing: 'easeOutExpo'
                });
            }
        },
        selectClickHandler(select) {
            const list = e => document.querySelectorAll(e);
            this.skillsMenu = this.skillsMenu.map(item => ({
                ...item,
                isActive: item.id===select.id ? true : false
            }));
            this.skillsMenu.forEach(item => {
                if(!item.isActive) {
                    this.$anime({
                        targets: this.$refs[item.ref][0].children[0],
                        color: 'rgb(211 211 211)',
                        easing: 'easeOutExpo'
                    });
                    this.$anime({
                        targets: this.$refs[item.ref][0].children[1],
                        width: '30%',
                        backgroundColor: 'rgb(211 211 211)',
                        easing: 'easeOutExpo'
                    });
                }
            });
            this.isLoading = true;
            const skill = select.name==='Front-End' ? 'html' : (select.name==="Back-End" ? 'php' : 'git');
            this.$axios.$get(`/api/skills/${skill}`)
            .then(res => {
                this.currentSkill(res);
            }).finally(() => {
                this.isLoading = false;
                this.$anime({
                    targets: list('.skills-site .skills-icons .skill'),
                    opacity: [0, 1],
                    easing: 'easeOutExpo',
                    delay: this.$anime.stagger(100)
                });
            }).catch(e => {})
        }
    }
}
</script>