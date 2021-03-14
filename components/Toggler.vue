<template>
  <button
    type="button"
    class="toggler"
    :pressed="pressed"
    v-on:click="pressed = pressed ? false : true"
  >
    <span class="vertical-menu-line"></span>
    <span class="vertical-menu-line"></span>
    <span class="vertical-menu-line"></span>
  </button>
</template>

<script scoped>
export default {
  data() {
    return {
      pressed: false
    };
  }
};
</script>

<style scoped lang="scss">
.toggler {
  background-color: transparent;
  border: none;
  width: 50px;
  height: 40px;

  &:focus {
    outline: none;
  }

  .vertical-menu-line {
    display: table-cell;
    transform: translateY(-100px);

    animation-name: fadeDown;
    animation-duration: 0.3s;
    animation-fill-mode: forwards;

    &:nth-child(1) {
      animation-delay: 0.4s;
    }
    &:nth-child(2) {
      animation-delay: 0.2s;
    }
    &:nth-child(3) {
      animation-delay: 0s;
    }

    width: 22px;
    height: 3px;
    background-color: #ffffff;
    display: block;
    margin: 4px auto;

    transition: all 200ms;
  }

  &:hover {
    .vertical-menu-line {
      &:first-child {
        transform: translateY(-2px);
      }
      &:last-child {
        transform: translateY(2px);
      }
    }
  }

  &[pressed="true"] {
    outline: none;

    .vertical-menu-line {
      &:first-child {
        transform: rotate(45deg) !important;
        margin-bottom: -3px;
      }
      &:nth-child(2) {
        display: unset;
      }
      &:last-child {
        transform: rotate(-45deg) !important;
        margin-top: 0px;
      }
    }
  }
}

@keyframes fadeDown {
  from {
    transform: translateY(-100px);
  }
  to {
    transform: translateX(0px);
  }
}
</style>
