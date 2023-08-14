<template>
  <footer class="footer">
    <div class="footer__container">
      <p class="footer__text">Разработано в КБ Челомей под лицензией №455-224ПМ</p>
    </div>
  </footer>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.footer {
  @include flexible(100%);
  justify-content: center;
  height: 100%;
  background-color: $color-background;

  &__container {
    @include flexible(100%);
    justify-content: center;
    align-items: center;
    box-sizing: border-box;
    max-width: $regular-width;
    padding: 20px 10px;
  }

  &__text {
    @include text(16px);
    padding: 0;
    color: $color-text-light;
  }
}
</style>
