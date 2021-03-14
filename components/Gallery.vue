<template>
  <div class="gallery">
    <slot> </slot>
    <!--
    <div class="gallery__item">
      <div class="embed">
        <img src="https://source.unsplash.com/collection/582659/1" />
      </div>
    </div>
    <div class="gallery__item">
      <div class="embed">
        <img src="https://source.unsplash.com/collection/582659/2" />
      </div>
    </div>
    <div class="gallery__item">
      <div class="embed">
        <img src="https://source.unsplash.com/collection/582659/3" />
      </div>
    </div>
    <div class="gallery__item gallery__item--v-2">
      <div class="embed embed--1-2">
        <img src="https://source.unsplash.com/collection/582659/4" />
      </div>
    </div>
    <div class="gallery__item">
      <div class="embed">
        <img src="https://source.unsplash.com/collection/582659/5" />
      </div>
    </div>
    <div class="gallery__item gallery__item--h-2">
      <div class="embed embed--2-1">
        <img src="https://source.unsplash.com/collection/582659/6" />
      </div>
    </div>-->
  </div>
</template>

<script scoped>
export default {
  props: {
    items: Array
  }
};
</script>

<style lang="scss" scoped>
* {
  box-sizing: border-box;
}

img {
  block-size: auto;
  max-inline-size: 100%;
  vertical-align: middle;
}

/* Gallery  */

.gallery {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(4, 1fr);

  @media (min-width: 992px) {
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
  }
  @media (min-width: 1200px) {
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(2, 1fr);
  }
}
</style>
