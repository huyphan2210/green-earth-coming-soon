<script setup lang="ts">
import { onMounted, ref } from "vue";
import burgerMenu from "../../assets/burger-menu.svg";
import Menu from "./Menu/Menu.vue";
import Logo from "../Logo/Logo.vue";

const isMenuShown = ref(false);
const toggleMenu = () => {
  isMenuShown.value = !isMenuShown.value;
};

const headerRef = ref<HTMLElement>();

onMounted(() => {
  const header = headerRef.value;
  header?.classList.toggle("appear");
});
</script>

<template>
  <header ref="headerRef">
    <Logo />
    <button type="button" class="burger-menu" :onclick="toggleMenu">
      <img :src="burgerMenu" loading="lazy" alt="Menu" />
    </button>
    <Menu :toggle-menu="toggleMenu" :is-menu-shown="isMenuShown" />
  </header>
</template>

<style lang="scss" scoped>
header {
  opacity: 0;
  padding: var(--padding);
  position: sticky;
  left: 0;
  top: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: white;
  min-height: var(--header-height);
  z-index: 1;

  .burger-menu {
    background-color: transparent;
  }
}

@media screen and (min-width: 64rem) {
  header {
    position: absolute;
    padding: 2.5rem 5rem;
    .burger-menu {
      display: none;
    }
  }
}
</style>
