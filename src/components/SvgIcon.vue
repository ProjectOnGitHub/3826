<template>
  <svg
    :class="iconClass"
    aria-hidden="true"
  >
    <use :xlink:href="iconName" />
  </svg>
</template>

<script>
export default {
  props: {
    iconName: {
      type: String,
      required: true
    },
    iconClass: {
      type: String,
      default: ''
    }
  }
};
</script>

<style lang="scss" scoped>
.icon {
  &__feature {
    width: 60px;
    height: 60px;
  }
}
</style>
