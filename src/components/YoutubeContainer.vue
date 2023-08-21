<template>
  <div class="youtube-container">
    <iframe
      class="youtube-container__iframe"
      :src="embedUrl"
      frameborder="0"
      allowfullscreen
    ></iframe>
  </div>
</template>

<script>
export default {
  props: {
    videoId: {
      type: String,
      required: true
    }
  },
  computed: {
    embedUrl() {
      return `https://www.youtube.com/embed/${this.videoId}`;
    }
  }
};
</script>
<style style lang="scss" scoped>
.youtube-container {
  position: relative;
  padding-bottom: 56.25%; /* 16:9 aspect ratio */
  height: 0;
  overflow: hidden;

  &__iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
  }
}
</style>
