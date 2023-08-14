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
        :class="setDotClass(item.id)"
        @click="selectDot(item.id)"
      ></li>
    </ul>
    <button
      class="carousel__button carousel__button_left"
      @click="prevSlide"
    >
      <svg-icon
        icon-name="arrow-left-icon"
        icon-class="icon carousel__icon-button"
      />
    </button>
    <button
      class="carousel__button carousel__button_right"
      @click="nextSlide"
    >
      <svg-icon
        icon-name="arrow-right-icon"
        icon-class="icon carousel__icon-button"
      />
    </button>
  </div>
</template>

<script>
import imagesMap from '../utils/images';
import SvgIcon from './SvgIcon.vue';

export default {
  components: { SvgIcon },
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
    },
    selectDot(item) {
      this.count = item - 1;
    },
    setDotClass(id) {
      return {
        'carousel__dots-item': true,
        'carousel__dots-item_selected': id - 1 === this.count
      };
    }
  }
};
</script>

<style lang="scss" scoped>
.carousel {
  @include gridable(100%);
  height: 100%;
  min-height: 650px;
  overflow: hidden;
  position: relative;
  @media screen and (max-width: $tablet) {
    min-height: 500px;
  }

  &__list {
    @include flexible(100%);
    @include unmarkedList();
    justify-self: center;
    transform: translateX(0);
    transition: all ease-in-out 0.5s;
    max-width: 1200px;

    &-item {
      @include flexible(100%);
      justify-content: center;
      flex-shrink: 0;
      position: relative;
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
    align-self: start;
    z-index: 10;

    &-item {
      cursor: pointer;
      @include unmarkedList();
      height: 5px;
      width: 40px;
      border: 1px solid $color-decorate;
      border-radius: 1px;
      transform: skewX(-38deg);
      background-color: rgba($color-decorate, 0.2);
      transition: all ease-in-out 0.5s;

      &_selected {
        background-color: rgba($color-decorate, 0.8);
      }
    }
  }

  &__image {
    height: auto;
    max-height: 700px;
    object-fit: cover;
    object-position: top;
    width: 100%;
  }

  &__info {
    @include gridable(100%);
    position: absolute;
    bottom: 30px;
    padding: 0 10px;
    box-sizing: border-box;
    gap: 10px;
    max-width: 500px;

    @media screen and (max-width: $tablet) {
      max-width: 300px;
    }
    @media screen and (max-width: $smartphone) {
      max-width: 250px;
    }
  }
  &__title {
    @include gridable(100%);
    font-size: 40px;
    margin: 0;
    color: $color-light;
    z-index: 10;
    position: relative;
    text-align: center;
    box-sizing: border-box;

    @media screen and (max-width: $tablet) {
      font-size: 24px;
    }

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
    color: $color-light;
    padding: 15px;
    position: relative;
    z-index: 10;
    margin: 0;
    box-sizing: border-box;

    @media screen and (max-width: $tablet) {
      font-size: 12px;
    }

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
    @include flexible(40px);
    margin: 15px;
    border-radius: 5px;
    background: transparent;
    align-self: center;
    z-index: 10;
    height: 40px;
    border-top: 2px solid $color-decorate;
    border-bottom: 2px solid $color-decorate;
    position: absolute;
    transform: translateX(0);

    &_left {
      justify-self: start;

      &:hover {
        transform: translateX(-5px);
      }
    }

    &_right {
      justify-self: end;
      &:hover {
        transform: translateX(5px);
      }
    }
  }

  &__icon-button {
    width: 40px;
    height: 40px;
    fill: $color-decorate;
  }
}
</style>
