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
    background: rgba(41, 41, 41, 0.6);
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
    top: -40px;
    right: -40px;
    width: 40px;
    height: 40px;
    background-color: $color-decorate;
    border: none;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;

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
      background-color: #d32f2f;
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
