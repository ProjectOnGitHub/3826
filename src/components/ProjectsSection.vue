<template>
  <base-section
    class-name="projects"
    :section-title="pageTitle"
  >
    <ul class="projects__list">
      <li
        v-for="project in projects"
        :key="project.id"
        class="project"
      >
        <figure class="project__figure">
          <img
            :alt="project.name"
            class="project__image"
            :src="images[`./projects/jpg/${project.image}`]"
          />
          <figcaption class="project__caption">
            <h2 class="project__title">
              {{ project.name }}
            </h2>
            <p class="project__text">
              {{ project.description }}
            </p>
          </figcaption>
        </figure>
      </li>
    </ul>
  </base-section>
</template>

<script>
import BaseSection from './BaseSection.vue';
import projects from '../data/projects';
import imagesMap from '../utils/images';

export default {
  components: { BaseSection },
  data() {
    return {
      projects,
      images: imagesMap,
      pageTitle: 'Наши проекты'
    };
  }
};
</script>

<style lang="scss" scoped>
.projects {
  max-width: $max-width;

  &__list {
    @include gridable(100%);
    @include unmarkedList;
    grid-template-columns: repeat(auto-fill, minmax(470px, 1fr));
    justify-content: center;
    grid-auto-rows: auto;
    gap: 1px;

    @media screen and (max-width: $smartphone) {
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    }
  }
}
.project {
  overflow: hidden;
  width: 100%;
  height: 475px;

  &__figure {
    @include flexible(100%);
    height: 100%;
    margin: 0;
    position: relative;
    cursor: pointer;

    &:hover .project__caption {
      @media #{$mouse-device} {
        visibility: visible;
        opacity: 1;
      }
    }
  }

  &__caption {
    @include flexible(100%);
    flex-direction: column;
    align-items: center;
    color: $color-light;
    justify-content: center;
    text-align: center;
    height: 100%;
    visibility: hidden;
    opacity: 0;
    gap: 13px;
    position: absolute;
    transition: 0.5s ease-in-out;
    background-color: rgba($color-background, 0.7);
  }

  &__image {
    object-fit: cover;
    width: 100%;
    height: auto;
    object-position: center;
  }

  &__title {
    @include title;
    font-size: 18px;
  }

  &__text {
    font-size: 16px;
    margin: 0;
  }
}
</style>
