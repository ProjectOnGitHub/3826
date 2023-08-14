<template>
  <header
    class="header"
    :class="{ header_fixed: isScrolled }"
  >
    <div
      class="header__container"
      :class="{ header__container_fixed: isScrolled }"
    >
      <a
        href="#about"
        class="logo"
      >
        <span class="logo__row logo__row_first">Предприятие</span>
        <span class="logo__row logo__row_second">3826</span>
      </a>
      <nav class="header__navigation">
        <button
          class="header__button"
          name="header-button"
          type="button"
          @click="toggleMenu"
        >
          <span
            class="cross"
            :class="{ cross_active: active }"
          >
            <span class="cross__line"></span>
          </span>
        </button>
        <div
          class="overlay"
          :class="{ overlay_opened: active }"
          @click="toggleMenu"
        ></div>
        <ul
          class="header__menu"
          :class="{ header__menu_opened: active }"
        >
          <li
            v-for="link in links"
            :key="link.id"
            class="header__menu-item"
            @click="toggleMenu"
          >
            <a
              class="header__menu-link"
              :href="`#${link.url}`"
            >
              {{ link.anchor }}
            </a>
          </li>
        </ul>
      </nav>
    </div>
  </header>
</template>

<script>
import links from '../data/links.js';
import imagesMap from '../utils/images';

export default {
  data() {
    return {
      active: false,
      links,
      images: imagesMap,
      isScrolled: false
    };
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
  },

  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    toggleMenu() {
      this.active = !this.active;
    },
    handleScroll() {
      this.isScrolled = window.scrollY > 0;
    }
  }
};
</script>

<style lang="scss" scoped>
.header {
  @include gridable(100%);
  grid-area: block;
  justify-items: center;
  box-sizing: border-box;
  height: $header-height;
  z-index: 15;
  transition: 0.2s ease-in-out;
  position: relative;

  &::after {
    content: '';
    justify-self: center;
    box-sizing: border-box;
    height: 1px;
    background-color: rgba($color-light, 0.15);
    position: absolute;
    bottom: 0;
    width: 100%;
    max-width: $regular-width;
  }

  &_fixed {
    position: fixed;
    background-color: rgba($color-background, 0.9);
    height: $header-height-fixed;

    &::after {
      max-width: none;
    }
  }

  &__container {
    @include gridable(100%);
    grid-template-columns: repeat(2, max-content);
    justify-content: space-between;
    align-items: center;
    box-sizing: border-box;
    max-width: calc(2 * $common-padding + $regular-width);
    padding: 0 $common-padding;
    transition: 0.2s ease-in-out;
  }

  &__button {
    display: none;
    justify-items: right;

    @media screen and (max-width: $tablet-large) {
      @include flexible(32px);
      @include button;
      position: relative;
      z-index: 20;
      height: 32px;
      padding: 0;
      background-color: transparent;
      background-size: contain;
      border: none;
      border-radius: 0;
    }
  }

  &__menu {
    @include flexible(100%);
    @include unmarkedList;
    gap: 20px 59px;
    align-content: center;
    font-size: 14px;
    font-weight: 500;
    text-transform: uppercase;

    @media screen and (max-width: $tablet-large) {
      position: fixed;
      top: 0;
      right: -320px;
      z-index: 10;
      justify-content: center;
      flex-direction: column;
      align-content: center;
      align-items: center;
      box-sizing: border-box;
      width: 100%;
      max-width: 320px;
      height: 100vh;
      font-size: 18px;
      background-color: $color-background;
      visibility: hidden;
      opacity: 0;
      transition: 0.5s;

      &_opened {
        right: 0;
        z-index: 15;
        visibility: visible;
        opacity: 1;
        transition: 0.5s;
      }
    }

    &-link {
      @include defaultLink;
      color: $color-light;

      &:hover {
        @media #{$mouse-device} {
          color: $color-decorate;
        }
      }
    }
  }
}
.cross {
  @include gridable(100%);
  align-content: space-between;
  box-sizing: border-box;
  width: 22px;
  height: 22px;

  &::before,
  &::after,
  & &__line {
    content: '';
    display: block;
    height: 2px;
    background: $color-light;
    border-radius: 2px;
    transition: 0.5s;
  }

  &_active {
    &::before {
      transform: translateY(10px) rotate(135deg);
    }

    &::after {
      transform: translateY(-9.5px) rotate(-135deg);
    }

    & .cross__line {
      transform: scale(0);
    }
  }
}

.logo {
  @include defaultLink;
  @include flexible(100%);
  flex-direction: column;
  align-items: center;

  &__row {
    text-transform: uppercase;
    line-height: 1;

    &_first {
      color: $color-light;
      letter-spacing: 0.8px;
      font-size: 10px;
    }

    &_second {
      color: $color-dark;
      font-weight: 900;
      font-size: 30px;
      letter-spacing: 1.2px;
      text-shadow: -1px -1px 0 $color-light, 1px -1px 0 $color-light, -1px 1px 0 $color-light,
        1px 1px 0 $color-light;
    }
  }
}

.overlay {
  display: none;
  @media screen and (max-width: $tablet-large) {
    position: fixed;
    top: 0;
    right: -150%;
    z-index: 15;
    display: block;
    width: 100%;
    height: 100vh;
    background: rgba($color-dark, 0.7);
    visibility: hidden;
    opacity: 0;
    transition: 0.5s;

    &_opened {
      left: 0;
      visibility: visible;
      cursor: pointer;
      opacity: 0.4;
      transition: 0.5s;
    }
  }
}
.icon {
  width: 50px;
  height: 50px;
}
</style>
