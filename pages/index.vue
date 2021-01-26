<template>
  <div class="container">
    <ParallaxBg />
    <MainMenu ref="menu" />
    <HomeSite ref="home" />
    <SkillsPage ref="skills" />
    <ProjectsPage ref="projects" />
    <AboutMe ref="aboutme" />
    <Experience />
    <Hobby />
    <Contact />
  </div>
</template>

<script>
export default {
    mounted() {
        const el = e => document.querySelector(e);
        const elList = e => document.querySelectorAll(e);
        const skillsHeader = el('.skills-site .header h2');
        const skillsMenu = el('.skills-site .skills-menu');
        const skillsIcons = el('.skills-site .skills-icons');
        const skillInfo = el('.skills-site .skill-info');
        const projectsHeader = el('.projects-site .header h2');
        const projects = elList('.projects-site .project');
        const aboutMeHeader = el('.aboutme-site .header h2');
        const aboutMeInfoLearning = elList('.aboutme-site .info-learning div p');
        const experienceHeader = el('.experience .header h2');
        const experienceTitleOne = el('.experience .list-one-title h3');
        const experienceListOne = elList('.experience .list-one li');
        const experienceTitleTwo = el('.experience .list-two-title h3');
        const experienceListTwo = elList('.experience .list-two li');
        const hobbyInfo = el('.hobby .info div p');
        window.addEventListener('scroll', () => {
            if(this.scrollCondition(skillsHeader)) skillsHeader.classList.add('active');
            if(this.scrollCondition(skillsMenu)) this.showScaleOpacityAnim(skillsMenu);
            if(this.scrollCondition(skillsIcons)) this.showScaleOpacityAnim(skillsIcons);
            if(skillInfo.getBoundingClientRect().top + (skillInfo.getBoundingClientRect().height / 2) <= window.innerHeight) skillInfo.classList.add('active');
            if(this.scrollCondition(projectsHeader)) projectsHeader.classList.add('active');
            projects.forEach(project => {
                if(project.getBoundingClientRect().top + (project.getBoundingClientRect().height / 2) <= window.innerHeight) project.classList.add('active');
            });
            if(this.scrollCondition(aboutMeHeader)) aboutMeHeader.classList.add('active');
            aboutMeInfoLearning.forEach(el => {
                if(this.scrollCondition(el)) el.classList.add('active');
            })
            if(this.scrollCondition(experienceHeader)) experienceHeader.classList.add('active');
            experienceListOne.forEach(el => {
                if(this.scrollCondition(el)) el.classList.add('active');
            })
            if(this.scrollCondition(experienceTitleOne)) experienceTitleOne.classList.add('active');
            experienceListTwo.forEach(el => {
                if(this.scrollCondition(el)) el.classList.add('active');
            })
            if(this.scrollCondition(experienceTitleTwo)) experienceTitleTwo.classList.add('active');
            if(this.scrollCondition(hobbyInfo)) hobbyInfo.classList.add('active');
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
          const sites = [ref('home'), ref('skills'), ref('projects'), ref('aboutme')];
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
