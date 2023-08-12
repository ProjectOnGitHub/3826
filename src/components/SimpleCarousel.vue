<template>
  <div class="carousel">
    <ul
      class="carousel__list"
      :style="{ transform: transform }"
    >
      <li
        v-for="item in items"
        :key="item.id"
        class="carousel__list-item"
      >
        <div class="carousel__info">
          <h2 class="carousel__title">
            {{ item.name }}
          </h2>
          <p class="carousel__text">
            {{ item.description }}
          </p>
        </div>
        <img
          :src="images[`./team/${item.image}`]"
          class="carousel__image"
        />
      </li>
    </ul>
    <ul class="carousel__dots">
      <li
        v-for="item in items"
        :key="item.id"
        class="carousel__dots-item carousel__dots-item_selected"
      ></li>
    </ul>
    <button
      class="carousel__button carousel__button_left"
      @click="prevSlide"
    >
      ←
    </button>
    <button
      class="carousel__button carousel__button_right"
      @click="nextSlide"
    >
      →
    </button>
  </div>
</template>

<script>
import imagesMap from '../utils/images';

export default {
  props: {
    items: {
      type: Array,
      default() {
        return [];
      }
    }
  },
  data() {
    return {
      images: imagesMap,
      count: 0
    };
  },
  computed: {
    transform() {
      return `translateX(${-this.count * 100}%)`;
    },
    totalSlides() {
      return this.items.length;
    }
  },
  methods: {
    prevSlide() {
      if (this.count <= 0) {
        this.count = this.totalSlides;
      }
      this.count--;
    },
    nextSlide() {
      if (this.count === this.totalSlides - 1) {
        this.count = -1;
      }
      this.count += 1;
    }
  }
};
</script>

<style lang="scss" scoped>
.carousel {
  @include gridable(100%);
  height: 100%;
  max-height: 700px;
  overflow: hidden;
  position: relative;
  max-width: 1200px;

  &__list {
    @include flexible(100%);
    @include unmarkedList();
    justify-self: center;
    transform: translateX(0);
    transition: all ease-in-out 0.5s;
    max-width: 1200px;

    &-item {
      flex-shrink: 0;
      position: relative;
      width: 100%;
      max-width: 1200px;
    }
  }

  &__dots {
    @include flexible(max-content);
    @include unmarkedList();
    padding: 15px;
    gap: 10px;
    position: absolute;
    justify-self: center;
    align-self: end;
    z-index: 20;

    &-item {
      @include unmarkedList();
      height: 5px;
      width: 40px;
      border: 1px solid $color-decorate;
      border-radius: 1px;
      transform: skewX(-38deg);
      background-color: rgba($color-decorate, 0.8);
    }
  }

  &__image {
    height: auto;
    max-height: 700px;
    object-fit: cover;
    object-position: top;
  }

  &__info {
    position: absolute;
    bottom: 30px;
    left: 30px;
  }

  &__title {
    @include gridable(110%);
    font-size: 48px;
    margin: 0;
    color: $color-light;
    z-index: 20;
    position: relative;
    justify-content: center;

    &::after {
      position: absolute;
      content: '';
      width: 100%;
      height: 100%;
      background-color: $color-decorate;
      transform: skewX(-8deg);
      z-index: -1;
    }
  }

  &__text {
    @include gridable(110%);
    font-size: 16px;
    width: 100%;
    max-width: 300px;
    color: $color-light;
    box-sizing: border-box;
    padding: 25px;
    position: relative;
    z-index: 20;
    &::after {
      position: absolute;
      content: '';
      width: 100%;
      height: 100%;
      background-color: rgba($color-dark, 0.8);
      transform: skewX(8deg);
      z-index: -1;
    }
  }

  &__button {
    @include button;
    @include flexible(60px);
    margin: 15px;
    border-radius: 5px;
    background-color: rgba($color-dark, 0.7);
    align-self: center;
    z-index: 20;
    height: 60px;
    border: 2px solid $color-decorate;
    position: absolute;

    &_left {
      justify-self: start;
    }

    &_right {
      justify-self: end;
    }
  }
}
</style>
