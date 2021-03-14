<template>
  <ul id="small-slider">
    <slot />

    <div v-if="listLength == 0">
      <span
        class="spinner-border spinner-border-sm"
        role="status"
        aria-hidden="true"
      ></span>
      <span>Cargando...</span>
    </div>
  </ul>
</template>

<script scoped>
export default {
  data() {
    return {
      round: 0,
      listLength: 0
    };
  },
  methods: {
    reloadItems() {
      console.log("reload");

      const cantidad = 5;
      const round = this.round * cantidad;

      const list = document.querySelectorAll("#small-slider > li");
      this.listLength = list.length;

      list.forEach(element => {
        element.classList.remove("active");
      });

      let x = 0;
      for (let i = 0; i < cantidad; i++) {
        if (round + i < list.length) {
          list[round + i].classList.add("active");
        }
      }

      if (list.length - 1 > (this.round + 1) * cantidad) {
        this.round++;
      } else {
        this.round = 0;
      }
    }
  },
  mounted() {
    this.reloadItems();
    setInterval(() => {
      this.reloadItems();
    }, 5000);
  }
};
</script>

<style lang="scss" scoped>
ul {
  width: 100%;
  max-width: 350px;
  padding: 0;
  display: flex;
  flex-wrap: wrap;

  li {
    width: 20%;
    list-style-type: none;
    opacity: 0;
    display: none;
    text-align: center;
    padding-right: 20px;

    * {
      width: 100%;
    }
  }
}

.active {
  display: block;
  animation-name: show;
  animation-duration: 4s;
  animation-fill-mode: forwards;
}

@keyframes show {
  0% {
    opacity: 0;
  }
  20% {
    opacity: 1;
  }
  80% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}
</style>
