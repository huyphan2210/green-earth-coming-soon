<script setup lang="ts">
import { ref } from "vue";
import burgerMenu from "../../assets/burger-menu.svg";
import Logo from "../Logo/Logo.vue";
import Menu from "./Menu/Menu.vue";

const isMenuShown = ref(false);
const toggleMenu = () => {
  isMenuShown.value = !isMenuShown.value;
};
</script>

<template>
  <header>
    <Logo />
    <button type="button" class="burger-menu" :onclick="toggleMenu">
      <img :src="burgerMenu" loading="lazy" alt="Menu" />
    </button>
    <Menu :toggle-menu="toggleMenu" v-if="isMenuShown" />
  </header>
</template>

<style lang="scss" scoped>
header {
  padding: var(--padding);
  position: sticky;
  left: 0;
  top: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: white;

  .burger-menu {
    background-color: transparent;
  }
}

@media screen and (min-width: 64rem) {
  header {
    padding: 2.5rem 5rem;
    .burger-menu {
      display: none;
    }
  }
}
</style>
