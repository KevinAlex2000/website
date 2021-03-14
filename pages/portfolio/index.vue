<template>
  <div class="container-fluid py-2">
    <gallery>
      <galleryItem
        v-for="(proyect, index) in proyects"
        :key="index"
        :img="proyect.cover"
        :embed="getSizeEmbed(index)"
        :galleryItemSize="getSizeGalleryItem(index)"
        :opacity="true"
      >
        <template v-slot:hover>
          <div
            class="w-100 p-5 position-absolute top-50 start-50 translate-middle text-center"
          >
            <NuxtLink
              :to="'portfolio/' + proyect.title"
              class="text-uppercase title"
            >
              {{ proyect.title }}
            </NuxtLink>
            <p
              class=" m-auto text-secondary fs-6 mt-4 description d-none d-md-block"
            >
              {{ proyect.description }}
            </p>
          </div>
          <!--
          <div>{{ proyect.title }}</div>-->
        </template>
      </galleryItem>
    </gallery>
  </div>
</template>

<script scoped>
export default {
  data() {
    return {
      proyects: []
    };
  },
  methods: {
    getProyects() {
      this.$axios.get("/data/proyects.json").then(response => {
        this.proyects = response.data;
      });
    },
    getSizeEmbed(index) {
      let embed = "";

      if ((index + 1) % 4 == 0) {
        embed = "embed--1-2";
      } else if ((index + 1) % 6 == 0) {
        embed = "embed--2-1";
      }

      return embed;
    },
    getSizeGalleryItem(index) {
      let gallery = "";

      if ((index + 1) % 4 == 0) {
        gallery = "gallery__item--v-2";
      } else if ((index + 1) % 6 == 0) {
        gallery = "gallery__item--h-2";
      }

      return gallery;
    }
  },
  created() {
    this.getProyects();
  }
};
</script>

<style lang="scss" scoped>
.title {
  color: var(--bs-dark);

  &:hover {
    color: var(--bs-primary);
  }
}

.description {
  max-width: 450px;
}
</style>
