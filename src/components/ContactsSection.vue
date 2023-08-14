<template>
  <base-section
    class-name="contacts"
    :section-title="pageTitle"
  >
    <div class="contacts__container">
      <ul class="contacts__list">
        <li class="contacts__list-item">
          <span class="contacts__list-item-name">Время работы:</span>
          понедельник-воскресенье, круглосуточно
        </li>
        <li class="contacts__list-item">
          <span class="contacts__list-item-name">Телефон:</span>
          <a
            class="contacts__link"
            href="tel:+772323826"
          >
            +7 (7232) 38-26
          </a>
        </li>
        <li class="contacts__list-item">
          <span class="contacts__list-item-name">Почтовый адрес:</span>
          КССР, Усть-Каменогорская область, НПП им. Кирова, а/я 3826
        </li>
        <li class="contacts__list-item">
          <span class="contacts__list-item-name">Электронный адрес:</span>
          <a
            class="contacts__link"
            href="mailto:info@3826.su"
          >
            info@3826.su
          </a>
        </li>
      </ul>
      <div class="contacts__map">
        <iframe
          src="https://yandex.ru/map-widget/v1/?um=constructor%3Ac693cf555911fe5611b81ea1ff36d19e6d76a0dbc7d81b67125754d71df0bc28&amp;source=constructor"
          width="100%"
          height="400"
          frameborder="0"
        ></iframe>
      </div>
    </div>
  </base-section>
</template>

<script>
import BaseSection from './BaseSection.vue';
import imagesMap from '../utils/images';

export default {
  components: { BaseSection },
  data() {
    return {
      images: imagesMap,
      pageTitle: 'Контакты'
    };
  }
};
</script>

<style lang="scss" scoped>
.contacts {
  &__container {
    @include gridable(100%);
    gap: 30px 15px;
    box-sizing: border-box;
    padding: 0 10px;
    max-width: $regular-width;
    grid-template-columns: 1fr 1fr;

    @media screen and (max-width: $tablet) {
      grid-template-columns: 1fr;
      padding: 0;
    }
  }

  &__list {
    @include gridable(100%);
    grid-template-columns: 1fr;
    align-content: start;
    @include unmarkedList;
    @include text(20px);
    color: $color-text-dark;
    gap: 20px 40px;

    @media screen and (max-width: $tablet) {
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      padding: 0 10px;
      box-sizing: border-box;
    }

    &-item {
      @include flexible(100%);
      flex-direction: column;
      gap: 5px;

      &-name {
        color: $color-text-light;
      }
    }
  }

  &__link {
    @include defaultLink;
    color: $color-decorate;
    width: max-content;

    &:hover {
      opacity: 0.8;
    }
  }
}
</style>
