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
      <hgroup>
        <h2>
          <span>Welcome to </span>
          <span>Green </span>
          <span>Earth</span>
        </h2>
        <p>
          At Green Earth, we’re passionate about gardening, sustainability, and
          helping you create a green oasis right at home. Whether you're a
          seasoned gardener or just starting out, we have everything you need to
          make your garden flourish.
        </p>
      </hgroup>
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
    padding-top: 2.4375rem;
    padding-inline: calc(var(--padding) * 2);

    hgroup {
      text-align: center;

      h2 {
        font-size: clamp(1.5rem, 2vw, 2rem);
        font-weight: 400;
        span {
          color: var(--green);
          &:first-child {
            color: var(--light-green);
          }
          &:last-child {
            color: var(--brown);
          }
        }
      }

      p {
        font-size: clamp(1rem, 1.5vw, 1.5rem);
        line-height: 1.5;
      }
    }
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
      padding-top: 12.5rem;
      width: calc(60% - var(--padding) * 2);

      hgroup {
        text-align: left;
      }
    }
  }
}
</style>
