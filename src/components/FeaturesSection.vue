<template>
  <base-section
    class-name="features"
    :section-title="pageTitle"
  >
    <ul class="features__list">
      <li
        v-for="feature in features"
        :key="feature.id"
        class="features__list-item"
      >
        <img
          :src="images[`./features/${feature.icon}`]"
          :alt="feature.title"
          class="features__icon"
        />
        <h3 class="features__subtitle">
          {{ feature.title }}
        </h3>
        <p class="features__text">
          {{ feature.text }}
        </p>
      </li>
    </ul>
  </base-section>
</template>

<script>
import BaseSection from './BaseSection.vue';
import features from '../data/features';
import imagesMap from '../utils/images';

export default {
  components: { BaseSection },
  data() {
    return {
      features,
      images: imagesMap,
      pageTitle: 'Преимущества'
    };
  }
};
</script>

<style lang="scss" scoped>
.features {
  padding: 0;

  &__list {
    @include flexible(100%);
    @include unmarkedList;
    justify-content: space-between;
    flex-wrap: wrap;
    max-width: $regular-width;
    row-gap: 74px;
    box-sizing: border-box;
    padding: 0 10px;

    @media screen and (max-width: $tablet-large) {
      max-width: 700px;
      column-gap: 40px;
    }

    @media screen and (max-width: $tablet-small) {
      justify-content: center;
      gap: 40px;
    }

    &-item {
      @include flexible(100%);
      gap: 25px;
      flex-direction: column;
      max-width: 296px;
      text-align: center;
      align-items: center;
    }
  }

  &__icon {
    width: 80px;
    height: 80px;
  }

  &__subtitle {
    @include titleH3;
    color: $color-text-dark;
  }

  &__text {
    @include text(20px);
    color: $color-text-light;
  }
}
</style>
