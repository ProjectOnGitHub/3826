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
        @touchstart="activateProject(project.id)"
      >
        <figure class="project__figure">
          <img
            :alt="project.name"
            class="project__image"
            :src="images[`./projects/jpg/${project.image}`]"
          />
          <figcaption
            :class="[
              'project__caption',
              { project__caption_active: activeProjectId === project.id }
            ]"
          >
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
      pageTitle: 'Проекты',
      activeProjectId: null
    };
  },
  methods: {
    activateProject(projectId) {
      if (this.activeProjectId === projectId) {
        this.activeProjectId = null;
      } else {
        this.activeProjectId = projectId;
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.projects {
  max-width: $max-width;

  &__list {
    @include gridable(100%);
    @include unmarkedList;
    grid-auto-rows: auto;
    grid-template-columns: repeat(auto-fill, minmax(460px, 1fr));
    justify-content: center;
    gap: 1px;

    @media screen and (max-width: $smartphone) {
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    }
  }
}
.project {
  width: 100%;
  height: 475px;
  overflow: hidden;

  &__figure {
    @include flexible(100%);
    position: relative;
    height: 100%;
    margin: 0;
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
    position: absolute;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    box-sizing: border-box;
    height: 100%;
    padding: 0 15px;
    text-align: center;
    color: $color-light;
    background-color: rgba($color-background, 0.7);
    visibility: hidden;
    opacity: 0;
    transition: 0.5s ease-in-out;
    gap: 13px;

    &_active {
      visibility: visible;
      opacity: 1;
    }
  }

  &__image {
    width: 100%;
    height: auto;
    object-fit: cover;
    object-position: center;
  }

  &__title {
    @include titleH3;
  }

  &__text {
    @include text(20px);
  }
}
</style>
