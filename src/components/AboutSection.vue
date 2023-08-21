<template>
  <base-section class-name="about">
    <div class="about__container">
      <h1 class="about__title">Меняем жизнь человечества к лучшему</h1>
      <p class="about__text">
        Всего один шаг отделяет нас от удивительного и невероятного эволюционного скачка, который
        полностью изменит весь мир, столь привычный нам с рождения!
      </p>
      <button
        class="about__button"
        name="about-button"
        type="button"
        aria-label="Find out more"
        @click="togglePopup"
      >
        Узнать больше
      </button>
    </div>
    <the-popup
      :is-open="isOpen"
      :toggle-popup="togglePopup"
    >
      <youtube-container video-id="0UBiw1xkHl8" />
    </the-popup>
  </base-section>
</template>

<script>
import BaseSection from './BaseSection.vue';
import ThePopup from './ThePopup.vue';
import YoutubeContainer from './YoutubeContainer.vue';

export default {
  components: { BaseSection, ThePopup, YoutubeContainer },
  data() {
    return {
      isOpen: false
    };
  },
  methods: {
    togglePopup() {
      this.isOpen = !this.isOpen;
    }
  }
};
</script>

<style lang="scss" scoped>
.about {
  position: relative;
  align-items: center;
  height: 100vh;
  background-image: url('../assets/images/background.png');
  background-repeat: no-repeat;
  background-size: cover;

  &::before {
    content: '';
    position: absolute;
    z-index: 0;
    box-sizing: border-box;
    width: 100%;
    height: 100vh;
    background-color: rgba($color-background, 0.7);
  }

  &__container {
    @include gridable(100%);
    z-index: 5;
    justify-items: center;
    box-sizing: border-box;
    max-width: calc(930px + $common-padding * 2);
    padding: $header-height $common-padding 0 $common-padding;
    color: $color-light;
  }

  &__title {
    @include titleH1;
    padding-bottom: 30px;
    line-height: 1.09;
  }

  &__text {
    @include text(22px);
    padding-bottom: 70px;
    text-align: center;
  }

  &__button {
    @include flexible(max-content);
    @include button();
    height: 58px;
    padding: 12px 36px;
    font-size: 27px;
    line-height: 1.61;
    color: $color-light;
    text-transform: uppercase;
    background-color: $color-dark;
    border: 3px solid $color-decorate;
    border-radius: 2px;

    &:hover {
      @media #{$mouse-device} {
        background-color: $color-decorate;
      }
    }
  }
}
</style>
