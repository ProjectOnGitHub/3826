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
      >
        Узнать больше
      </button>
    </div>
  </base-section>
</template>

<script>
import BaseSection from './BaseSection.vue';

export default { components: { BaseSection } };
</script>

<style lang="scss" scoped>
.about {
  height: 100vh;
  background-repeat: no-repeat;
  align-items: center;
  background-size: cover;
  background-image: url('../assets/images/background.png');
  position: relative;

  &::before {
    content: '';
    z-index: 0;
    box-sizing: border-box;
    position: absolute;
    background-color: rgba($color-background, 0.7);
    height: 100vh;
    width: 100%;
  }

  &__container {
    @include gridable(100%);
    justify-items: center;
    max-width: calc(930px + $common-padding * 2);
    z-index: 5;
    padding: $header-height $common-padding 0 $common-padding;
    box-sizing: border-box;
    color: $color-light;
  }

  &__title {
    @include titleH1;
    line-height: 1.09;
    padding-bottom: 30px;
  }

  &__text {
    @include text(22px);
    text-align: center;
    padding-bottom: 70px;
  }

  &__button {
    @include flexible(max-content);
    @include button();
    height: 58px;
    padding: 12px 36px;
    border-radius: 2px;
    font-size: 27px;
    line-height: 1.61;
    text-transform: uppercase;
    border: 3px solid $color-decorate;
    color: $color-light;
    background-color: $color-dark;

    &:hover {
      @media #{$mouse-device} {
        background-color: $color-decorate;
      }
    }
  }
}
</style>
