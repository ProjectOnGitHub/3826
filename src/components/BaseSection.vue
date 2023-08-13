<template>
  <section
    :id="className"
    class="section"
    :class="className"
  >
    <h2
      v-if="sectionTitle"
      :class="`section__title ${className}__title`"
    >
      {{ sectionTitle }}
    </h2>
    <slot></slot>
  </section>
</template>

<script>
export default {
  props: {
    className: {
      type: String,
      default: ''
    },
    sectionTitle: {
      type: String,
      default: ''
    }
  }
};
</script>

<style lang="scss" scoped>
.section {
  @include gridable(100%);
  justify-items: center;
  box-sizing: border-box;

  &__title {
    padding: 70px 20px 40px 20px;
    font-size: 76px;
    font-weight: 400;
    margin: 0;
    text-transform: uppercase;
    @media screen and (max-width: $tablet) {
      font-size: 48px;
    }
  }
}
</style>
