<template>
    <nav>
        <div class="logo"></div>
        <div class="icons">
            <div class="mail" @click="contactHandler"></div>
            <div class="linkedin"></div>
            <div class="github"></div>
        </div>
        <div :class="isLangOpen ? 'lang active' : 'lang'">
            <div class="selected" @click="clickLangHandler">
                <div ref="currentLang" class="icon"></div>
                <div class="arrow"></div>
            </div>
            <div ref="otherLang" class="choose"></div>
        </div>
        <div class="mobile-menu" @click="activeMobileMenu">
            <div></div>
            <div></div>
            <div></div>
        </div>
        <OverlayMenu v-if="isMobileActive" @close-mobile-menu="closeMobileMenu" />
    </nav>
</template>

<script>
export default {
    data() {
        return {
            isLangOpen: false,
            isMobileActive: false
        }
    },
    mounted() {
        this.$refs.currentLang.classList.add('pl');
        this.$refs.otherLang.classList.add('uk');
    },
    methods: {
        contactHandler() {
            const el = e => document.querySelector(e);
            const contact = el('.contact-site').getBoundingClientRect(); 
            el('.contact-site').scrollIntoView({ behavior: 'smooth' });
            setTimeout(() => el('.contact-site form label:first-of-type input').focus(), contact.top > 500 ? 1000 : 400);
        },
        activeMobileMenu() {
            this.isMobileActive = true;
        },
        closeMobileMenu() {
            this.isMobileActive = false;
        },
        clickLangHandler() {
            this.isLangOpen = !this.isLangOpen;
        }
    }
}
</script>
