<template>
    <div class="container">
        <ParallaxBg />
        <ToTop :isTopButtonActive="isTopButtonActive" />
        <MainMenu ref="menu" :lang="lang" @change-lang="changeLang" />
        <HomeSite ref="home" :lang="lang" />
        <SkillsPage ref="skills" :lang="lang" />
        <ProjectsPage ref="projects" :lang="lang" />
        <About ref="about" :lang="lang" />
        <Contact ref="contact" :lang="lang" />
        <Footer ref="footer" :isTopButtonActive="isTopButtonActive" :lang="lang" />
    </div>
</template>

<script>
export default {
    data() {
        return {
            isTopButtonActive: false,
            isLoading: true,
            lang: ''
        }
    },
    created() {
        this.changeLang();
    },
    mounted() {
        const el = e => document.querySelector(e);
        const elList = e => document.querySelectorAll(e);
        window.addEventListener('scroll', () => {
            this.isTopButtonActive = this.toggleTopButton();
            const addClassEl = [
                el('.skills-site .header h2'), el('.projects-site .header h2'), el('.aboutme-site .header h2'), el('.experience .header h2'), el('.experience .list-one-title h3'), el('.experience .list-two-title h3'), el('.hobby .info div p'), el('.contact-site .header h2'), el('.contact-site .info p'), el('.contact-site form button')
            ];
            addClassEl.forEach(item => {
                if(this.scrollCondition(item)) item.classList.add('active')
            });
            const addClassElLists = [
                elList('.aboutme-site .info-learning div p'), elList('.experience .list-one li'), elList('.experience .list-two li'), elList('.contact-site form label')
            ];
            addClassElLists.forEach(item => {
                item.forEach(el => {
                    if(this.scrollCondition(el)) el.classList.add('active');
              })
            })
            const skillsLists = [
                el('.skills-site .skills-menu'), el('.skills-site .skills-icons')
            ];
            skillsLists.forEach(item => {
                if(this.scrollCondition(item)) this.showScaleOpacityAnim(item);
            })
            if(el('.skills-site .skill-info').getBoundingClientRect().top + (el('.skills-site .skill-info').getBoundingClientRect().height / 2) <= window.innerHeight) el('.skills-site .skill-info').classList.add('active');
            elList('.projects-site .project').forEach(project => {
                if(project.getBoundingClientRect().top + (project.getBoundingClientRect().height / 2) <= window.innerHeight) project.classList.add('active');
            });
            this.setActiveLink();
        });
    },
    methods: {
        changeLang(lang) {
            if(this.$cookies.get('lang')) {
                if(lang) {
                    this.$cookies.set('lang', lang, { path: '/', maxAge: 60*60*24*7 })
                } else {
                    this.$cookies.set('lang', this.$cookies.get('lang'), { path: '/', maxAge: 60*60*24*7 })
                }
            } else {
                this.$cookies.set('lang', 'uk', { path: '/', maxAge: 60*60*24*7 })
            }
            this.lang = this.$cookies.get('lang');
        },
        toggleTopButton() {
            const homeBottom = this.$refs.home.$el.getBoundingClientRect().bottom;
            const footerBottom = this.$refs.footer.$el.getBoundingClientRect().bottom;
            return (homeBottom <= (window.innerHeight / 2)) && (footerBottom > (window.innerHeight + 50)) ? 
                true : false
        },
        showScaleOpacityAnim(element) {
            element.children.forEach((item, index) => {
                setTimeout(() => item.classList.add('visible'), (200 * index))
                // this.$anime({
                //     targets: item,
                //     opacity: 1,
                //     easing: 'easeOutExpo',
                //     delay: index * 100,
                // })
            })
        },
        scrollCondition(element) {
            return element.getBoundingClientRect().bottom <= window.innerHeight;
        },
        setActiveLink() {
            const el = e => document.querySelector(e);
            const ref = e => this.$refs[e];
            const sites = [ref('home'), ref('skills'), ref('projects'), ref('about'), ref('contact')];
            sites.forEach((ref, index) => {
                const rect = ref.$el.getBoundingClientRect();
                const menuHeight = this.$refs.menu.$el.getBoundingClientRect().height;
                const desktopLink = el(`nav .desktop-menu>div:nth-of-type(${index + 1})`);
                const overlayLink = el('.overlay-menu-list') ? el(`.overlay-menu-list li:nth-of-type(${index + 1})`) : null;
                if(rect.top <= menuHeight && rect.bottom >= menuHeight) {
                    el('.overlay-menu-list') ? overlayLink.classList.add('active') : null;
                    desktopLink.classList.add('active');
                } else {
                    el('.overlay-menu-list') ? overlayLink.classList.remove('active') : null;
                    desktopLink.classList.remove('active');
                }
            });
        }
    },
    head() {
        return {
            title: 'Portfolio',
            meta: [
                {
                    hid: 'description',
                    name: 'description',
                    content: 'This is my portfolio created with nuxt in 2021.'
                }
            ]
        }
    }
}
</script>

<style>

</style>
