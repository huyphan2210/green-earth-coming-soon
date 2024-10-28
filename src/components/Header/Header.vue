<script setup lang="ts">
import Logo from "../Logo/Logo.vue";
import burgerMenu from "../../assets/burger-menu.svg";
</script>

<template>
  <header>
    <Logo />
    <button type="button" class="burger-menu">
      <img :src="burgerMenu" loading="lazy" alt="Menu" />
    </button>
  </header>
</template>

<style lang="scss" scoped>
header {
  padding: 1rem;
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
