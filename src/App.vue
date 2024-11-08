<script setup lang="ts">
import { ref } from "vue";
import Footer from "./components/Footer/Footer.vue";
import Header from "./components/Header/Header.vue";
import Heading from "./components/Heading/Heading.vue";
import SubscriptionBox from "./components/SubscriptionBox/SubscriptionBox.vue";

const isSubscriptionBoxShown = ref(false);
const openSubscriptionBox = () => {
  isSubscriptionBoxShown.value = true;
};

const closeSubscriptionBox = () => {
  isSubscriptionBoxShown.value = false;
};
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
      <button type="button" v-on:click="openSubscriptionBox">Subscribe</button>
      <Footer is-from-content />
    </section>
    <SubscriptionBox
      :show-subscription-box="isSubscriptionBoxShown"
      :close-subscription-box="closeSubscriptionBox"
    />
  </main>
  <Footer :is-from-content="false" />
</template>

<style lang="scss" scoped>
main {
  margin-bottom: auto;
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
    padding: 2.4375rem 3.375rem;
    padding-inline: calc(var(--padding) * 2);

    hgroup {
      text-align: center;
      margin-block: 2.625rem;
      h2 {
        font-size: clamp(1.5rem, 2vw, 2rem);
        font-weight: 400;
        margin-block: 0 1.25rem;
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
        margin-block: 0;
      }
    }

    button {
      margin: auto;
      display: block;
      background-color: var(--pastel-yellow);
      padding: 1rem 3rem;
      color: var(--mustard-brown);
      border-radius: 0.25rem;
      font-size: 1rem;
      transition: 0.3s;

      &:hover {
        border-radius: 1rem;
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
      max-width: 42rem;
      .image {
        display: none;
        &.desktop {
          display: inline;
        }
      }
    }

    .content {
      padding-top: 12.5rem;
      flex: 1;

      hgroup {
        text-align: left;
      }
      button {
        margin: 0;
      }
    }
  }
}
</style>
