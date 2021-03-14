<template>
  <form
    id="contact-form"
    action="https://webapi-kevinalex.herokuapp.com/contacts"
    method="post"
    class="row"
    v-on:submit="sendContact"
  >
    <div class="col-md-6 mb-3">
      <input
        type="text"
        name="name"
        class="form-control"
        placeholder="Nombre"
        aria-label="Nombre"
        required
      />
    </div>
    <div class="col-md-6 mb-3">
      <input
        type="email"
        name="mail"
        class="form-control"
        placeholder="Email"
        aria-label="Email"
        required
      />
    </div>
    <div class="col-md-12 mb-3">
      <input
        type="text"
        name="subject"
        class="form-control"
        placeholder="Asunto"
        aria-label="Asunto"
        required
      />
    </div>
    <div class="col-md-12 mb-3">
      <textarea
        name="message"
        class="form-control"
        rows="8"
        placeholder="Mensaje"
        required
      ></textarea>
    </div>
    <div class="col-md-12">
      <button type="submit" class="btn btn-success px-4">
        <span v-if="!contactLoading">Enviar Mensaje</span>

        <div class="loading" v-if="contactLoading">
          <span
            class="spinner-border spinner-border-sm position-relative"
            role="status"
            aria-hidden="true"
            style="top: -3px"
          ></span>
          Cargando...
        </div>
      </button>

      <div v-if="contactName" class="mt-3 alert alert-success btn-sm">
        Gracias por contactarme {{ contactName }}. Te respondere los mas pronto
        que pueda.
      </div>
    </div>
  </form>
</template>

<script scoped>
export default {
  name: "form-contact",
  data() {
    return {
      contactLoading: false,
      contactName: null
    };
  },
  methods: {
    sendContact(event) {
      event.preventDefault();
      this.contactLoading = true;
      let formData = new FormData(event.target);

      const form = document.getElementById("contact-form");
      const url = form.getAttribute("action");

      let data = {};
      formData.forEach((value, key) => (data[key] = value));

      this.$axios
        .post(url, data)
        .then(response => {
          this.contactName = response.data.name;
          this.contactLoading = false;
        })
        .catch(e => {
          alert(
            "A ocurrido un error inesperado, vuelva a intentarlo mas tarde"
          );
          console.log(e);
          this.contactLoading = false;
        });

      form.reset();
    }
  },
  mounted() {}
};
</script>
