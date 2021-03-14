<template>
  <div class="container-fluid">
    <div class="row py-5 px-3">
      <div class="col-md-6">
        <div class="px-md-4 mx-md-4 px-xl-5 mx-xl-5">
          <div class="display-5 fw-bolder mb-5">
            Contactos
          </div>
          <div class="text-secondary">
            <p>
              Estoy interesado en oportunidades de autónomos, especialmente
              proyectos ambiciosos o grandes. Sin embargo, si tiene otra
              solicitud o pregunta, no dude en ponerse en contacto conmigo
              mediante el formulario a continuación.
            </p>

            <formContact />

            <p class="mt-5">
              Tambien puedes enviarme un
              <a :href="'mailto:' + mail">mail</a> o
              <a :href="'tel:' + phone">llamarme</a>
            </p>
          </div>
        </div>
      </div>

      <div class="col-md-12 d-block d-md-none mt-5">
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d62467.133612499034!2d-77.12877949176539!3d-11.891446630036564!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x9105d39b15cfb90d%3A0xe832fbc8423fbf88!2sVentanilla!5e0!3m2!1ses!2spe!4v1611003620380!5m2!1ses!2spe"
          class="map"
          frameborder="0"
          allowfullscreen=""
          aria-hidden="false"
          tabindex="0"
        ></iframe>
      </div>
    </div>

    <div class="cover-content position-fixed top-0 end-0 d-none d-md-block">
      <iframe
        src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d62467.133612499034!2d-77.12877949176539!3d-11.891446630036564!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x9105d39b15cfb90d%3A0xe832fbc8423fbf88!2sVentanilla!5e0!3m2!1ses!2spe!4v1611003620380!5m2!1ses!2spe"
        class="map"
        frameborder="0"
        allowfullscreen=""
        aria-hidden="false"
        tabindex="0"
      ></iframe>
    </div>
  </div>
</template>

<script scoped>
export default {
  name: "Contact",
  data() {
    return {
      mail: "",
      phone: ""
    };
  },
  methods: {
    getContactCall() {
      this.$axios.get("/data/profile.json").then(response => {
        console.log(response.data);
        this.mail = response.data.mail;
        this.phone = response.data.phone;
      });
    }
  },
  created() {
    this.getContactCall();
  }
};
</script>

<style lang="scss" scoped>
.cover-content {
  width: 45%;
  height: 100vh;
}
.map {
  width: 100%;
  height: 100%;
}
.list-group-item {
  font-size: 15px;
  border-radius: 0px;
  border: 0px;
  border-left: 2px solid rgb(173, 173, 173);
  color: rgb(110, 110, 110);

  &.active {
    background-color: #42b98334;
    color: var(--color-3);
    border-left: 2px solid var(--bs-primary);
  }
}

ul {
  padding-left: 0px;
  li {
    list-style: none;
    &:before {
      content: "•́";
      font-weight: 700;
      margin-right: 10px;
      color: var(--bs-primary);
    }
  }
}
</style>
