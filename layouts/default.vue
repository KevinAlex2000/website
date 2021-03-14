<template>
  <div>
    <!-- Nav que se muestra en pantalla mediana -->
    <nav
      :class="{ active: isPressed }"
      class="navbar-md navbar-dark fixed-top d-none d-lg-block"
    >
      <toggler id="toggler" />
      <div class="content text-center">
        <logo width="100px" class=" mt-5 mb-4" />

        <ul class="menu my-5 text-uppercase">
          <li>
            <NuxtLink to="/">inicio</NuxtLink>
          </li>
          <li>
            <NuxtLink to="/about">sobre mi</NuxtLink>
          </li>
          <li>
            <NuxtLink to="/skills">skills</NuxtLink>
          </li>
          <li>
            <NuxtLink to="/portfolio">portafolio</NuxtLink>
          </li>
          <li>
            <NuxtLink to="/contact">contacto</NuxtLink>
          </li>
        </ul>

        <ul class="social-links mt-5">
          <li v-for="social in socialLinks" :key="social.name">
            <a target="_blank" :href="social.link">
              <font-awesome-icon :icon="['fab', social.name]" />
            </a>
          </li>
        </ul>
        <div class="text-secondary fs-6 mb-5 text-nowrap">
          Kevin Peña © 2021
        </div>
      </div>

      <ul class="social-links-bottom">
        <li v-for="social in socialLinks" :key="social.name">
          <a target="_blank" :href="social.link">
            <font-awesome-icon :icon="['fab', social.name]" />
          </a>
        </li>
      </ul>
    </nav>

    <!-- Nav que se muestra en pantalla chica -->
    <nav
      id="nav-pantalla-chica"
      class="navbar navbar-expand-lg navbar-dark bg-dark d-block d-lg-none"
    >
      <div class="container-fluid">
        <toggler
          data-bs-toggle="collapse"
          data-bs-target="#navbarSmall"
          aria-controls="navbarSmall"
          aria-expanded="false"
          aria-label="Toggle navigation"
        />

        <div class="collapse navbar-collapse p-3" id="navbarSmall">
          <div class="navbar-nav text-capitalize">
            <router-link to="/">inicio</router-link>
            <router-link to="/about">sobre mi</router-link>
            <router-link to="/skills">skills</router-link>
            <router-link to="/portfolio">portafolio</router-link>
            <router-link to="/contact">contacto</router-link>
          </div>
        </div>
      </div>
    </nav>
    <div id="container-principal">
      <Nuxt />
    </div>
  </div>
</template>

<script scoped>
export default {
  data() {
    return {
      socialLinks: [],
      isPressed: false
    };
  },
  methods: {
    // Calculando el tamaño del contenedor principal en pantalla chica
    calculateHeightScreen(event) {
      const containerPrincipal = document.getElementById("container-principal");

      if (992 > window.innerWidth) {
        const navPantallaChica = document.getElementById("nav-pantalla-chica");
        const alturaNav = navPantallaChica.clientHeight;

        const altura = window.innerHeight - alturaNav;
        containerPrincipal.style.cssText = "min-height: " + altura + "px";
        console.log("altura calculada");
      } else {
        containerPrincipal.style.cssText = "min-height: 100vh";
      }
    },
    getSocialLinks() {
      this.$axios.get("/data/social-links.json").then(response => {
        this.socialLinks = response.data;
      });
    }
  },
  mounted() {
    this.getSocialLinks();

    const app = this;

    const toggler = document.getElementById("toggler");
    toggler.addEventListener("click", () => {
      app.isPressed = app.isPressed ? false : true;
    });

    this.calculateHeightScreen();
    window.onresize = this.calculateHeightScreen;
  }
};
</script>
<style lang="scss" scoped>
.nuxt-link-exact-active {
  color: var(--bs-primary) !important;
}

#container-principal {
  @media (min-width: 992px) {
    margin-left: 70px;
  }
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
}

nav {
  z-index: 10000;
  a {
    color: var(--bs-light);
  }
}

.navbar-md {
  background-color: var(--bs-dark);
  transition: width 200ms;
  width: 70px;
  height: 100vh;
  overflow: hidden;

  #toggler {
    margin-top: 10px;
    margin-left: 10px;
  }

  .content {
    transition: opacity 100ms;
    position: relative;
    opacity: 0;

    .social-links {
      display: inline-flex;
      li {
        font-size: 14px;
        margin-right: 20px;

        &:last-child {
          margin-right: 0px;
        }

        a:hover {
          color: var(--bs-primary);
        }
      }
    }

    ul {
      padding-left: 0px;

      &.menu {
        font-size: 12px;
        font-weight: bolder;
        letter-spacing: 3px;

        li {
          margin-top: 30px;
        }
      }

      li {
        a {
          white-space: nowrap;
          &:hover {
            color: var(--bs-primary);
          }
        }
        list-style: none;
      }
    }
  }

  .social-links-bottom {
    position: absolute;
    width: 70px;
    bottom: 15px;
    list-style: none;
    padding-left: 0px;
    text-align: center;
    font-size: 14px;
    animation: translateRight100 0.4s;

    li {
      margin-top: 9px;

      a {
        color: var(--bs-light);
        &:hover {
          cursor: pointer;
          color: var(--bs-primary);
        }
      }
    }
  }

  &.active {
    overflow-y: auto;
    width: 250px;

    .content {
      opacity: 1;
    }

    .social-links-bottom {
      animation: translateLeft100 0.4s;
      transform: translateX(-50px);
    }
  }

  // Scrolled
  &::-webkit-scrollbar {
    width: 5px;
  }
  &::-webkit-scrollbar-track {
    background-color: var(--bs-dark);
  }
  &::-webkit-scrollbar-thumb {
    background-color: rgb(58, 58, 58);
  }
}

@keyframes translateLeft100 {
  0% {
    transform: translateX(0px);
  }
  100% {
    transform: translateX(-100px);
  }
}
@keyframes translateRight100 {
  0% {
    transform: translateX(-100px);
  }
  100% {
    transform: translateX(0px);
  }
}
</style>
