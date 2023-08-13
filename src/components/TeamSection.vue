<template>
  <base-section
    class-name="team"
    :section-title="pageTitle"
  >
    <simple-carousel :items="team" />
  </base-section>
</template>

<script>
import BaseSection from './BaseSection.vue';
import team from '../data/team';
import SimpleCarousel from './SimpleCarousel.vue';

export default {
  components: { BaseSection, SimpleCarousel },
  data() {
    return {
      team,
      pageTitle: 'Команда'
    };
  }
};
</script>

<style lang="scss" scoped>
.team {
  width: 100%;
  max-width: $regular-width;
  box-sizing: border-box;
}
</style>
