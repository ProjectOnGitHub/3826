<template>
  <main class="main">
    <about-section />
    <features-section />
    <projects-section />
    <team-section />
  </main>
</template>

<script>
import AboutSection from './AboutSection.vue';
import FeaturesSection from './FeaturesSection.vue';
import ProjectsSection from './ProjectsSection.vue';
import TeamSection from './TeamSection.vue';

export default { components: { AboutSection, FeaturesSection, ProjectsSection, TeamSection } };
</script>

<style lang="scss" scoped>
.main {
  @include gridable(100%);
  grid-area: block;
  justify-items: center;
}
</style>
