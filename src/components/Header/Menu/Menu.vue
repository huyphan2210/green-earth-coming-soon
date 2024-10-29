<script lang="ts" setup>
import { onUnmounted, ref } from "vue";
import closeIcon from "../../../assets/close-icon.svg";

const props = defineProps<{
  toggleMenu: () => void;
}>();

const { toggleMenu } = props;

const menuOverlayRef = ref<HTMLDivElement | null>();
const menuRef = ref<HTMLMenuElement | null>();

const toggleClosing = () => {
  const menuOverlay = menuOverlayRef.value;
  const menu = menuRef.value;
  if (menuOverlay && menu) {
    menuOverlay.classList.toggle("closing");
    menu.classList.toggle("closing");
  }
};

const closeMenu = () => {
  toggleClosing();
  setTimeout(() => toggleMenu(), 300);
};

onUnmounted(() => {
  toggleClosing();
});
</script>

<template>
  <div ref="menuOverlayRef" class="menu-overlay">
    <menu ref="menuRef" class="menu">
      <button class="close-icon" type="button" :onclick="closeMenu">
        <img :src="closeIcon" loading="lazy" alt="Close icon" />
      </button>
      <h2>This place is still a mystery</h2>
    </menu>
  </div>
</template>

<style lang="scss" scoped>
.menu-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: var(--background-overlay);
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  opacity: 0;
  animation: 0.3s ease-in-out forwards;
  animation-name: appear;
  &.closing {
    animation-name: disappear;
  }

  .menu {
    padding: var(--padding);
    flex: 1;
    width: 80%;
    max-width: 18.75rem;
    background-color: var(--lime-green);
    margin: 0;
    transform: translateX(100%);
    animation: 0.3s ease-in-out forwards;
    animation-name: slideIn;
    text-align: right;
    position: relative;
    &.closing {
      animation-name: slideOut;
    }

    .close-icon {
      background: transparent;
      margin-top: 29.5px;
      transform: translateY(-50%);
    }

    h2 {
      font-family: "Playwrite US Trad", sans-serif;
      text-align: center;
      white-space: nowrap;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%) rotate(-60deg);
      font-weight: 400;
      color: var(--light-brown);
      font-size: 2rem;
    }
  }
}

@keyframes appear {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}

@keyframes disappear {
  0% {
    opacity: 1;
  }

  100% {
    opacity: 0;
  }
}

@keyframes slideIn {
  0% {
    transform: translateX(100%);
  }

  100% {
    transform: translateX(0);
  }
}

@keyframes slideOut {
  0% {
    transform: translateX(0);
  }

  100% {
    transform: translateX(100%);
  }
}

@media screen and (min-width: 64rem) {
  .menu-overlay {
    display: none;
  }
}
</style>
