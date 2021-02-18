<template>
    <nav>
        <div class="logo"></div>
        <div class="desktop-menu">
            <div v-for="(item, index) in list" :key="index">
                <a :href="`/${item.name[lang]}`" @click.prevent="clickToScroll(item.name.uk)">
                    {{ item.name[lang] }}
                </a>
                <div></div>
            </div>
        </div>
        <div class="icons">
            <div 
                v-for="(icon, index) in icons" 
                :key="index" 
                :style="`background-image: url(${icon.path})`"
                @click="clickIconHandler(icon)"
            ></div>
        </div>
        <div :class="isLangOpen ? 'lang active' : 'lang'">
            <div class="selected" @click="clickLangHandler">
                <div ref="currentLang" :class="lang==='uk' ? 'icon uk' : 'icon pl'"></div>
                <div class="arrow"></div>
            </div>
            <div ref="otherLang" :class="lang==='uk' ? 'choose pl' : 'choose uk' " @click="changeCurrentLang"></div>
        </div>
        <div class="mobile-menu" @click="activeMobileMenu">
            <div></div>
            <div></div>
            <div></div>
        </div>
        <OverlayMenu 
            v-if="isMobileActive" 
            :lang="lang"
            :list="list"
            @close-mobile-menu="closeMobileMenu"
            :currentLinkActive="currentLinkActive"
            :clickToScroll="clickToScroll"
        />
    </nav>
</template>

<script>
export default {
    props: [
        'lang'
    ],
    data: () => ({
        icons: [
            {name: 'mail', path: require('~/assets/img/mail.svg')},
            {name: 'linkedin', path: require('~/assets/img/linkedin.svg'), link: 'linkedin.com/in/tmdev85'},
            {name: 'github', path: require('~/assets/img/github.svg'), link: 'github.com/TM85dev'},
        ],
        list: [
            {name: { uk: 'Home', pl: 'Strona Główna' }},
            {name: { uk: 'Skills', pl: 'Umiejętności' }},
            {name: { uk: 'Projects', pl: 'Projekty' }},
            {name: { uk: 'About Me', pl: 'O Mnie' }},
            {name: { uk: 'Contact', pl: 'Kontakt' }},
        ],
        isLangOpen: false,
        isMobileActive: false,
    }),
    mounted() {
        this.currentLinkActive('nav .desktop-menu>div');
    },
    methods: {
        clickToScroll(name) {
            const el = name.replace(' ', '').toLowerCase();
            document.querySelector(`.${el}-site`).scrollIntoView({behavior: 'smooth'});
            if(name.toLowerCase()==='contact') {
                const elDOM = e => document.querySelector(e);
                const contact = elDOM('.contact-site').getBoundingClientRect(); 
                setTimeout(() => elDOM('.contact-site form label:first-of-type input').focus(), contact.top > 500 ? 1000 : 400);
            }
        },
        currentLinkActive(menu) {
            const elDOM = el => document.querySelector(el);
            const sites = [elDOM('.home-site'), elDOM('.skills-site'), elDOM('.projects-site'), elDOM('.about-site'), elDOM('.contact-site')];
            sites.forEach((ref, index) => {
                const rect = ref.getBoundingClientRect();
                const link = document.querySelector(`${menu}:nth-of-type(${index + 1})`);
                const menuHeight = elDOM('nav').getBoundingClientRect().height;
                if(rect.top <= menuHeight && rect.bottom >= menuHeight) {
                    link.classList.add('active');
                } else {
                    link.classList.remove('active');
                }
            });
        },
        clickIconHandler(icon) {
            if(icon.name === 'mail') {
                const el = e => document.querySelector(e);
                const contact = el('.contact-site').getBoundingClientRect(); 
                el('.contact-site').scrollIntoView({ behavior: 'smooth' });
                setTimeout(() => el('.contact-site form label:first-of-type input').focus(), contact.top > 500 ? 1000 : 400);
            } else {
                window.open(`https://${icon.link}`, '_blank');
            }
        },
        activeMobileMenu() {
            this.isMobileActive = true;
        },
        closeMobileMenu() {
            this.isMobileActive = false;
        },
        clickLangHandler() {
            this.isLangOpen = !this.isLangOpen;
        },
        changeCurrentLang(e) {
            let lang = '';
            const currentLang = e.target.classList[1];
            if(currentLang === 'uk') {
                lang = 'uk';
                this.$refs.currentLang.classList = 'icon uk';
                this.$refs.otherLang.classList = 'choose pl';
            } else {
                lang = 'pl';
                this.$refs.currentLang.classList = 'icon pl';
                this.$refs.otherLang.classList = 'choose uk';
            }
            this.$emit('change-lang', lang);
            this.clickLangHandler();
        }
    }
}
</script>
