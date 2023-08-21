<template>
  <transition name="popup-fade">
    <div
      v-if="isOpen"
      class="popup"
    >
      <div
        class="popup__overlay"
        @click="togglePopup"
      ></div>
      <div class="popup__container">
        <button
          class="popup__button-close"
          @click="togglePopup"
        ></button>
        <slot></slot>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    isOpen: {
      type: Boolean,
      default: false
    },

    togglePopup: {
      type: Function,
      default: () => {}
    }
  }
};
</script>
<style lang="scss" scoped>
.popup {
  @include flexible(100%);
  position: fixed;
  top: 0;
  left: 0;
  z-index: 200;
  justify-content: center;
  align-items: center;
  height: 100vh;
  cursor: pointer;
  transition: 0.5s;

  &__overlay {
    position: absolute;
    z-index: 9;
    width: 100%;
    height: 100%;
    background: rgba($color-text-dark, 0.6);
    transition: background 0.5s;
  }

  &__container {
    position: relative;
    width: 70%;
    height: auto;
    z-index: 300;
  }

  &__button-close {
    position: absolute;
    top: -24px;
    right: -24px;
    width: 24px;
    height: 24px;
    background-color: $color-decorate;
    border: none;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    transition: 0.5s ease-in-out;
    transform: rotate(0deg);

    &:hover {
      transform: rotate(180deg);
    }

    &::before,
    &::after {
      content: '';
      position: absolute;
      width: 60%;
      height: 2px;
      background-color: $color-light;
    }

    &::before {
      transform: rotate(45deg);
    }

    &::after {
      transform: rotate(-45deg);
    }

    &:hover {
      background-color: rgba($color-decorate, 0.8);
    }
  }

  &-fade {
    &-enter-active,
    &-leave-active {
      transition: opacity 0.5s;
    }

    &-enter,
    &-leave-to {
      opacity: 0;
    }
  }
}
</style>
