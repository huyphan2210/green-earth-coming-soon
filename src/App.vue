<script setup lang="ts">
import Header from "./components/Header/Header.vue";
import Heading from "./components/Heading/Heading.vue";
</script>

<template>
  <Header />
  <main>
    <section class="image-wrapper">
      <img
        class="image"
        src="./assets/images/image-mobile.png"
        loading="lazy"
        alt="Image"
      />
      <img
        class="image desktop"
        src="./assets/images/image-desktop.png"
        loading="lazy"
        alt="Image"
      />
    </section>
    <section class="content">
      <Heading />
    </section>
  </main>
  <footer></footer>
</template>

<style lang="scss" scoped>
main {
  .image-wrapper {
    display: flex;
    .image {
      width: 100%;
      &.desktop {
        display: none;
      }
    }
  }

  .content {
    padding-inline: calc(var(--padding) * 2);
  }
}

@media screen and (min-width: 64rem) {
  main {
    display: flex;
    flex-direction: row-reverse;
    flex: 1;
    .image-wrapper {
      width: 40%;
      .image {
        display: none;
        &.desktop {
          display: inline;
        }
      }
    }

    .content {
      width: calc(60% - var(--padding) * 2);
    }
  }
}
</style>
