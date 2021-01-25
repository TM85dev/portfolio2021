<template>
  <div class="container">
    <ParallaxBg />
    <MainMenu ref="menu" />
    <HomeSite ref="home" />
    <SkillsPage ref="skills" />
    <ProjectsPage ref="projects" />
  </div>
</template>

<script>
export default {
    mounted() {
        const skillsHeader = document.querySelector('.skills-site .header h2');
        const skillsMenu = document.querySelector('.skills-site .skills-menu');
        const skillsIcons = document.querySelector('.skills-site .skills-icons');
        const skillInfo = document.querySelector('.skills-site .skill-info');
        const projectsHeader = document.querySelector('.projects-site .header h2');
        const projects = document.querySelectorAll('.projects-site .project');
        window.addEventListener('scroll', () => {
            if(this.scrollCondition(skillsHeader)) skillsHeader.classList.add('active');
            if(this.scrollCondition(skillsMenu)) this.showScaleOpacityAnim(skillsMenu);
            if(this.scrollCondition(skillsIcons)) this.showScaleOpacityAnim(skillsIcons);
            if(skillInfo.getBoundingClientRect().top + (skillInfo.getBoundingClientRect().height / 2) <= window.innerHeight) skillInfo.classList.add('active');
            if(this.scrollCondition(projectsHeader)) projectsHeader.classList.add('active');
            projects.forEach(project => {
              if(project.getBoundingClientRect().top + (project.getBoundingClientRect().height / 2) <= window.innerHeight) project.classList.add('active');
            });
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
        if(el('.overlay-menu-list')) {
          const sites = [this.$refs.home, this.$refs.skills, this.$refs.projects];
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
