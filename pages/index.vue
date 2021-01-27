<template>
  <div class="container">
    <ParallaxBg />
    <ToTop :isTopButtonActive="isTopButtonActive" />
    <MainMenu ref="menu" />
    <HomeSite ref="home" />
    <SkillsPage ref="skills" />
    <ProjectsPage ref="projects" />
    <About ref="about" />
    <Contact ref="contact" />
    <Footer ref="footer" :isTopButtonActive="isTopButtonActive" />
  </div>
</template>

<script>
export default {
    data() {
      return {
          isTopButtonActive: false
      }
    },
    mounted() {
        const el = e => document.querySelector(e);
        const elList = e => document.querySelectorAll(e);

        window.addEventListener('scroll', () => {
            this.isTopButtonActive = (this.$refs.home.$el.getBoundingClientRect().bottom <= window.innerHeight / 2 && this.$refs.footer.$el.getBoundingClientRect().bottom > (window.innerHeight + 50)) ? true : false;
            if(this.scrollCondition(el('.skills-site .header h2'))) el('.skills-site .header h2').classList.add('active');
            if(this.scrollCondition(el('.skills-site .skills-menu'))) this.showScaleOpacityAnim(el('.skills-site .skills-menu'));
            if(this.scrollCondition(el('.skills-site .skills-icons'))) this.showScaleOpacityAnim(el('.skills-site .skills-icons'));
            if(el('.skills-site .skill-info').getBoundingClientRect().top + (el('.skills-site .skill-info').getBoundingClientRect().height / 2) <= window.innerHeight) el('.skills-site .skill-info').classList.add('active');
            if(this.scrollCondition(el('.projects-site .header h2'))) el('.projects-site .header h2').classList.add('active');
            elList('.projects-site .project').forEach(project => {
                if(project.getBoundingClientRect().top + (project.getBoundingClientRect().height / 2) <= window.innerHeight) project.classList.add('active');
            });
            if(this.scrollCondition(el('.aboutme-site .header h2'))) el('.aboutme-site .header h2').classList.add('active');
            elList('.aboutme-site .info-learning div p').forEach(el => {
                if(this.scrollCondition(el)) el.classList.add('active');
            })
            if(this.scrollCondition(el('.experience .header h2'))) el('.experience .header h2').classList.add('active');
            elList('.experience .list-one li').forEach(el => {
                if(this.scrollCondition(el)) el.classList.add('active');
            })
            if(this.scrollCondition(el('.experience .list-one-title h3'))) el('.experience .list-one-title h3').classList.add('active');
            elList('.experience .list-two li').forEach(el => {
                if(this.scrollCondition(el)) el.classList.add('active');
            })
            if(this.scrollCondition(el('.experience .list-two-title h3'))) el('.experience .list-two-title h3').classList.add('active');
            if(this.scrollCondition(el('.hobby .info div p'))) el('.hobby .info div p').classList.add('active');
            if(this.scrollCondition(el('.contact-site .header h2'))) el('.contact-site .header h2').classList.add('active');
            if(this.scrollCondition(el('.contact-site .info p'))) el('.contact-site .info p').classList.add('active');
            elList('.contact-site form label').forEach(el => {
                if(this.scrollCondition(el)) el.classList.add('active');
            })
            if(this.scrollCondition(el('.contact-site form button'))) el('.contact-site form button').classList.add('active');
            this.setActiveLink();
        });
    },
  methods: {
      showScaleOpacityAnim(element) {
          element.children.forEach((item, index) => {
              this.$anime({
                  targets: item,
                  opacity: 1,
                  easing: 'easeOutExpo',
                  delay: index * 100
              })
          })
      },
      scrollCondition(element) {
          return element.getBoundingClientRect().bottom <= window.innerHeight;
      },
      setActiveLink() {
        const el = e => document.querySelector(e);
        const ref = e => this.$refs[e];
        if(el('.overlay-menu-list')) {
          const sites = [ref('home'), ref('skills'), ref('projects'), ref('about'), ref('contact')];
          sites.forEach((ref, index) => {
            const rect = ref.$el.getBoundingClientRect();
            const link = el(`.overlay-menu-list li:nth-of-type(${index + 1})`);
            const menuHeight = this.$refs.menu.$el.getBoundingClientRect().height;
            if(rect.top <= menuHeight && rect.bottom >= menuHeight) {
                link.classList.add('active');
            } else {
                link.classList.remove('active');
            }
          });
        }
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
