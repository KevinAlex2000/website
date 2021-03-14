<template>
  <div class="container-fluid">
    <div class="row py-5 px-3">
      <div class="col-md-12">
        <div class="display-4 fw-bolder">
          ¡Hola!
          <br />
          <span class="text-primary">Mi nombre es Kevin.</span>
        </div>
        <div class="justify-content-center row my-4">
          <p class="fs-5 col-xl-4 col-lg-6 text-secondary">
            <span class="fw-bold">Programador junior</span>
            con más de 1 año de experiencia en el desarrollo de software.
          </p>
        </div>
        <div class="links">
          <router-link
            to="/portfolio"
            class="btn btn-outline-primary rounded-0 me-2"
          >
            Portafolio
          </router-link>
          <router-link
            to="/contact"
            class="btn btn-outline-secondary rounded-0"
          >
            Contáctame
          </router-link>
        </div>
      </div>
      <!--
      <div class="col-md-12">
        <img
          src="http://www.aidiapp.com/wp-content/uploads/2019/07/pc-768x488.png"
          class="mt-4"
          style="width: 300px"
        />
      </div>
      -->
      <!--
      <div class="col-md-4">
        <img
          class="w-100"
          src="http://www.aidiapp.com/wp-content/uploads/2019/07/pc-768x488.png"
          alt=""
        />
      </div>
      -->
    </div>
  </div>
</template>

<script scoped>
export default {};
</script>

<style lang="scss" scoped>
.container-fluid {
  text-align: center;
  /*
  @media (min-width: 992px) {
    min-height: 100vh;
    margin: 0 auto;
    display: flex;
    justify-content: center;
    align-items: center;
  }*/
}

.btn-outline-secondary {
  &:hover {
    background-color: #6c757d2a;
    color: var(--bs-secondary);
  }
}
.btn-outline-primary {
  &:hover {
    background-color: #20c99621;
    color: var(--bs-primary);
  }
}
</style>
