<script lang="ts" setup>
import { ref, watch } from "vue";
import pinkFlower from "../../assets/pink-flower.svg";
import sunFlower from "../../assets/sunflower.svg";

const props = defineProps<{
  showSubscriptionBox: boolean;
  closeSubscriptionBox: () => void;
}>();

const subsciptionBoxRef = ref<HTMLDialogElement>();

const handleClickDialog = (e: MouseEvent) => {
  const dialog = e.currentTarget as HTMLDialogElement;

  const rect = dialog.getBoundingClientRect();
  const isInDialog =
    e.clientX >= rect.left &&
    e.clientX <= rect.right &&
    e.clientY >= rect.top &&
    e.clientY <= rect.bottom;

  if (!isInDialog) {
    dialog.classList.toggle("disappear");
    setTimeout(() => {
      props.closeSubscriptionBox();
      dialog.classList.toggle("disappear");
    }, 400);
  }
};

watch(
  () => props.showSubscriptionBox,
  (isShown) => {
    const subsciptionBox = subsciptionBoxRef.value;
    if (isShown) {
      subsciptionBox?.showModal();
    } else {
      subsciptionBox?.close();
    }
  }
);
</script>

<template>
  <dialog ref="subsciptionBoxRef" :onclick="handleClickDialog">
    <img class="pink-flower" :src="pinkFlower" loading="lazy" alt="Pink Flower" />
    <img class="sunflower" :src="sunFlower" loading="lazy" alt="Sunflower" />
    <h2>Coming soon - Get Ready to grow!</h2>
    <p>
      Our doors will open soon! Be the first to know about our grand opening and
      exclusive offers by signing up for our newsletter below.
    </p>
    <form>
      <input type="email" placeholder="Please type your email here..." />
    </form>
  </dialog>
</template>

<style lang="scss" scoped>
dialog {
  position: relative;
  width: calc(100vw - 4.625rem);
  max-width: 40rem;
  padding: 1.3125rem;
  border: none;
  border-radius: 0.5rem;
  background: linear-gradient(270deg, var(--pastel-yellow), var(--green));
  animation: 0.3s ease-in-out forwards;
  animation-name: appear;
  overflow: visible;

  &::backdrop {
    background: rgba($color: black, $alpha: 25%);
    animation: 0.3s ease-in-out forwards;
    animation-name: appear;
  }

  &.disappear {
    animation-name: disappear;
    &::backdrop {
      animation-name: disappear;
    }
  }
  
  .pink-flower {
    position: absolute;
    right: 0;
    top: 0;
    transform: translateY(-50%);
  }

  .sunflower {
    position: absolute;
    right: 0;
    bottom: 0;
    transform: translateY(50%);
  }

  h2 {
    margin-block: 0 1.5rem;
    font-size: 1.5rem;
    font-weight: 400;
    color: var(--beige);
    width: 80%;
    max-width: 23.5625rem;
  }

  p {
    margin-block: 0 1.125rem;
    line-height: 1.5;
    color: white;
    max-width: 27.1875rem;
  }

  form {
    input {
      width: 70%;
      max-width: 30rem;
      font-size: 1rem;
      padding: 1rem;
      border-radius: 0.25rem;

      &:focus {
        outline: none;
      }
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
</style>
