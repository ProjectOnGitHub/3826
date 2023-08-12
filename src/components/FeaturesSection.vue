<template>
  <base-section class-name="features">
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
      images: imagesMap
    };
  }
};
</script>

<style lang="scss" scoped>
.features {
  padding: 120px 0;

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
      gap: 25px;
      flex-direction: column;
      max-width: 296px;
      text-align: center;
    }
  }

  &__icon {
    margin-bottom: 10px;
    height: 80px;
    object-fit: contain;
  }

  &__title {
    @include title;
    font-size: 14px;
    color: $color-title-dark;
  }

  &__text {
    font-size: 14px;
    line-height: 1.5;
    font-weight: 400;
    margin: 0;
    color: $color-text-dark;
  }
}
</style>
