<template>
  <section
    :id="className"
    class="section"
    :class="className"
  >
    <slot></slot>
  </section>
</template>

<script>
export default {
  props: {
    className: {
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
}
</style>
