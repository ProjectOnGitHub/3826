<template>
  <main class="main">
    <about-section />
    <features-section />
    <projects-section />
  </main>
</template>

<script>
import AboutSection from './AboutSection.vue';
import FeaturesSection from './FeaturesSection.vue';
import ProjectsSection from './ProjectsSection.vue';

export default { components: { AboutSection, FeaturesSection, ProjectsSection } };
</script>

<style lang="scss" scoped>
.main {
  @include gridable(100%);
  grid-area: block;
  justify-items: center;
}
</style>
