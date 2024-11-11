<script lang="ts" setup>
import { onUnmounted, ref, watch } from "vue";
import closeIcon from "../../../assets/close-icon.svg";

const props = defineProps<{
  toggleMenu: () => void;
  isMenuShown: boolean;
}>();

const { toggleMenu } = props;

const menuOverlayRef = ref<HTMLDialogElement | null>();
const menuRef = ref<HTMLMenuElement | null>();

const toggleClosing = () => {
  const menuOverlay = menuOverlayRef.value;
  if (menuOverlay) {
    menuOverlay.classList.toggle("closing");
  }
};

const closeMenu = () => {
  toggleClosing();
  setTimeout(() => toggleMenu(), 300);
};

const handleClickDialog = (e: MouseEvent) => {
  if (e.srcElement !== e.currentTarget) return;
  const dialog = e.currentTarget as HTMLDialogElement;

  const rect = dialog.getBoundingClientRect();
  const isInDialog =
    e.clientX >= rect.left &&
    e.clientX <= rect.right &&
    e.clientY >= rect.top &&
    e.clientY <= rect.bottom;

  if (!isInDialog) {
    toggleClosing();
  }
};

onUnmounted(() => {
  toggleClosing();
});

watch(
  () => props.isMenuShown,
  (isShown) => {
    const menuOverlay = menuOverlayRef.value;
    if (isShown) {
      menuOverlay?.showModal();
    } else {
      menuOverlay?.close();
      menuOverlay?.classList.toggle("closing");
    }
  }
);
</script>

<template>
  <dialog ref="menuOverlayRef" class="menu-overlay" @click="handleClickDialog">
    <menu ref="menuRef" class="menu">
      <button class="close-icon" type="button" @click="closeMenu">
        <img :src="closeIcon" loading="lazy" alt="Close icon" />
      </button>
      <h2>This place is still a mystery</h2>
    </menu>
  </dialog>
</template>

<style lang="scss" scoped>
.menu-overlay {
  transform: translateX(100%);
  animation: 0.3s ease-in-out forwards;
  animation-name: slideIn;
  min-height: 100dvh;
  width: 80%;
  max-width: 18.75rem;
  border: none;
  margin: 0;
  top: 0;
  left: 0;
  margin-left: auto;
  padding: 0;
  &::backdrop {
    animation: 0.3s ease-in-out forwards;
    animation-name: appear;
    background-color: var(--background-overlay);
  }
  &[open] {
    display: flex;
    flex-direction: column;
  }
  &:focus-visible {
    outline: none;
  }

  &.closing {
    animation-name: slideOut;
    &::backdrop {
      animation-name: disappear;
    }
  }

  .menu {
    padding: var(--padding);
    background-color: var(--lime-green);
    margin: 0;
    text-align: right;
    position: relative;
    flex: 1;

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
