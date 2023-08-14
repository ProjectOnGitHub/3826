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
        <h2 class="features__title">
          {{ feature.title }}
        </h2>
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
    max-width: 1076px;
    row-gap: 74px;

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
      flex-direction: column;
      align-items: center;
      max-width: 296px;
      text-align: center;
      gap: 25px;
    }
  }

  &__icon {
    width: 80px;
    height: 80px;
  }

  &__title {
    @include titleH2;
    color: $color-text-dark;
  }

  &__text {
    color: $color-text-light;
  }
}
</style>
