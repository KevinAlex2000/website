<template>
  <div class="container-fluid">
    <div class="row py-5 px-3">
      <div class="col-md-6">
        <div class="px-md-4 mx-md-4 px-xl-5 mx-xl-5">
          <div class="display-5 fw-bolder mb-5">
            Mis habilidades
          </div>
          <div class="text-secondary">
            <p>
              El área principal de mi experiencia es el desarrollo web.
            </p>
            <p>
              Node JS, Express, MySQL son las herramientas que utilizo la
              mayoria de veces para el lado del backend y HTML, CSS, javascript,
              Vue JS para el lado del frontend.
            </p>
            <p>
              Tambien tengo experiencia desarrollando programas de escritorio
              con Visual Studio .Net (C#)
            </p>
            <p>
              Echale un vistazo a mi Curriculum para ver detalles o contactame
              ahora
            </p>
            <smallSlider class="mt-5">
              <li v-for="(tecnology, index) in tecnologies" :key="index">
                <img
                  :src="tecnology.url"
                  class="tooltip-element"
                  data-bs-toggle="tooltip"
                  data-bs-placement="bottom"
                  :title="tecnology.name"
                />
              </li>
            </smallSlider>
          </div>
        </div>
      </div>

      <div class="col-md-12 d-block d-md-none mt-5">
        <img
          src="https://www.tecnomental.com/wp-content/uploads/2018/08/importancia-saber-programacion.jpg"
          class="w-100"
        />
      </div>
    </div>

    <div
      class="cover-content position-fixed top-0 end-0 d-none d-md-block"
    ></div>
  </div>
</template>

<script scoped>
export default {
  data() {
    return {
      tecnologies: []
    };
  },
  methods: {
    getTecnologies() {
      this.$axios.get("/data/tecnologies.json").then(response => {
        this.tecnologies = response.data;
      });
    }
  },
  created() {
    this.getTecnologies();
  }
};
</script>

<style lang="scss" scoped>
.cover-content {
  width: 45%;
  height: 100vh;
  background-image: url(https://www.tecnomental.com/wp-content/uploads/2018/08/importancia-saber-programacion.jpg);
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
