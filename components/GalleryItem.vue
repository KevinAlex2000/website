<template>
  <div :class="'gallery__item ' + galleryItemSize">
    <div :class="'embed ' + embed">
      <div class="bg-img">
        <img :src="img" :class="{ opacity: opacity }" />
        <slot name="hover"></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    img: String,
    embed: {
      type: String,
      default: ""
    },
    galleryItemSize: {
      type: String,
      default: ""
    },
    opacity: {
      type: Boolean,
      default: false
    }
  }
};
</script>

<style lang="scss" scoped>
.bg-img {
  background-color: rgb(224, 224, 224);
  img {
    transition: all 0.7s;

    &.opacity {
      opacity: 0.15;
    }
  }

  &:hover {
    img {
      opacity: 0.03;
    }
  }
}

.bg-img,
.hover {
  cursor: pointer;
  * {
    cursor: pointer;
  }
}

/* Embed */

.embed {
  overflow: hidden;
  padding-block-start: 100%;
  position: relative;
}

.embed--1-2 {
  padding-top: calc(100% / (1 / 2));
}

.embed--2-1 {
  padding-top: calc(100% / (2 / 1));
}

.embed--2-3 {
  padding-top: calc(100% / (2 / 3));
}

.embed > * {
  height: 100%;
  left: 0;
  margin: 0.25em;
  position: absolute;
  top: 0;
  width: 100%;

  img {
    height: 100%;
    left: 0;
    object-fit: cover;
    position: absolute;
    top: 0;
    width: 100%;
  }
}

.gallery__item--h-2 {
  grid-column-end: span 2;
}

.gallery__item--h-3 {
  grid-column-end: span 3;
}

.gallery__item--v-2 {
  grid-row-end: span 2;
}

.gallery__item--v-3 {
  grid-row-end: span 3;
}
</style>
