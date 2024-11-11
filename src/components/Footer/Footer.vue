<script setup lang="ts">
import Logo from "../Logo/Logo.vue";
import linkedInIcon from "../../assets/linked-in.svg";
import githubIcon from "../../assets/github.svg";
import figmaIcon from "../../assets/figma.svg";
import portfolioIcon from "../../assets/portfolio.svg";
import { onMounted, ref } from "vue";

const navigations = [
  {
    name: "LinkedIn",
    src: linkedInIcon,
    href: "https://www.linkedin.com/in/huy-phan-7924aa25a/",
  },
  {
    name: "Github",
    src: githubIcon,
    href: "https://github.com/huyphan2210",
  },
  {
    name: "Figma",
    src: figmaIcon,
    href: "https://www.figma.com/@huy33",
  },
  {
    name: "Portfolio",
    src: portfolioIcon,
    href: "https://huy-phan-portfolio.netlify.app/",
  },
];

const props = defineProps<{
  isFromContent: boolean;
}>();

const footerRef = ref<HTMLElement>();
onMounted(() => {
  const footer = footerRef.value;
  footer?.classList.toggle("appear");
});
</script>

<template>
  <footer ref="footerRef" :class="props.isFromContent ? 'from-content' : ''">
    <div class="footer-logo-wrapper">
      <Logo />
    </div>
    <nav>
      <a
        v-for="(navigation, index) in navigations"
        :key="index"
        :href="navigation.href"
        :title="navigation.name"
        target="_blank"
      >
        <img :src="navigation.src" loading="lazy" :alt="navigation.name" />
      </a>
    </nav>
  </footer>
</template>

<style lang="scss" scoped>
footer {
  opacity: 0;
  background-image: linear-gradient(90deg, var(--lime-green), var(--green));
  padding: var(--padding);
  display: flex;
  justify-content: space-between;
  align-items: center;
  nav {
    display: flex;
    gap: 1rem;
    a img {
      height: clamp(2rem, 5vw, 3rem);
      vertical-align: middle;
    }
  }
  &.from-content {
    display: none;
  }
}

@media screen and (min-width: 64rem) {
  footer {
    display: none;
    padding-inline: calc(var(--padding) * 2);
    padding-block: 1.5rem;
    .footer-logo-wrapper {
      display: none;
    }

    &.from-content {
      display: block;
      position: absolute;
      left: 0;
      bottom: 0;
      width: calc(100% - (var(--padding) * 4));
    }
  }
}
</style>
