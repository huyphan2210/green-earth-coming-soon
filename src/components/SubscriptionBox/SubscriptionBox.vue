<script lang="ts" setup>
import { ref, watch } from "vue";

const props = defineProps<{
  showSubscriptionBox: boolean;
}>();

const subsciptionBoxRef = ref<HTMLDialogElement>();

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
  <dialog ref="subsciptionBoxRef">
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
  width: calc(100vw - 4.625rem);
  max-width: 40rem;
  padding: 1.3125rem;
  border: none;
  border-radius: 0.5rem;
  background: linear-gradient(270deg, var(--pastel-yellow), var(--green));
  &::backdrop {
    background: rgba($color: black, $alpha: 25%);
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
  }
  
  form {
    input {
      width: 70%;
      max-width: 30rem;
      font-size: 1rem;
      padding: 1rem;
    }
  }
}
</style>
