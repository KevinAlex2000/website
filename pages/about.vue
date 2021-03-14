<template>
  <div class="container-fluid">
    <div class="row py-5 px-3">
      <div class="col-md-6">
        <div class="px-md-4 mx-md-4 px-xl-5 mx-xl-5">
          <div class="display-5 fw-bolder mb-5">
            Sobre Mi
          </div>
          <div class="text-secondary">
            <p>
              Mi nombre es Kevin Peña, un desarrollador de software con sede en
              Ventanilla-Lima, Peru.
            </p>
            <p>
              Mi pasión es crear aplicaciones que solucionen un conflicto. Tengo
              como objetivo siempre crear productos que satisfagan en totalidad
              a clientes.
            </p>
            <p>
              Graduado del instituto SENATI busco un lugar donde ejercer mis
              conocimientos y experiencia adquirida.
            </p>

            <div class="fw-600 my-4">
              <span class="text-primary">Experiencia</span> laboral:
            </div>
          </div>

          <div class="row">
            <div class="col-xl-3 mt-3">
              <div class="list-group" id="list-tab" role="tablist">
                <a
                  v-for="(item, index) in experience"
                  :key="item.business"
                  class="list-group-item list-group-item-action"
                  :class="{ active: index == 0 }"
                  data-bs-toggle="list"
                  :href="'#list-' + item.business"
                  role="tab"
                >
                  {{ item.business }}
                </a>
              </div>
            </div>
            <div class="col-xl-9 mt-3">
              <div class="tab-content" id="nav-tabContent">
                <div
                  v-for="(item, index) in experience"
                  :key="index"
                  class="tab-pane fade show"
                  :class="{ active: index == 0 }"
                  :id="'list-' + item.business"
                  role="tabpanel"
                  :aria-labelledby="'list-' + item.business + '-list'"
                >
                  {{ item.job }}
                  <a target="_blank" href="https://redneurocom.com/"
                    >@ {{ item.business }}</a
                  >
                  <div class="fs-6 text-secondary">
                    {{ item.since }} - {{ item.until }}
                  </div>

                  <ul class="fs-6 text-secondary mt-3">
                    <li v-for="homework in item.chores" :key="homework">
                      {{ homework }}
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="col-md-12 d-block d-md-none mt-5">
        <img
          src="https://demo.qodeinteractive.com/bridge103/wp-content/uploads/2015/05/about.jpg"
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
      experience: []
    };
  },
  methods: {
    getExperience() {
      this.$axios.get("/data/experience.json").then(response => {
        this.experience = response.data;
      });
    }
  },
  mounted() {
    this.getExperience();
  }
};
</script>

<style lang="scss" scoped>
.cover-content {
  width: 45%;
  height: 100vh;
  background-image: url(https://demo.qodeinteractive.com/bridge103/wp-content/uploads/2015/05/about.jpg);
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
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
