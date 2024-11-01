<template>
  <h1>
    <span class="top">WE'RE</span>
    <br />
    <span class="middle">COMING</span>
    <br />
    <span class="bottom">SOON</span>
  </h1>
</template>

<style lang="scss" scoped>
h1 {
  font-family: "Nico Moji", sans-serif;
  font-size: clamp(3rem, 4vw, 4.25rem);
  line-height: 1.5;
  max-width: 31.875rem;
  margin-block: 0 1rem;
  margin-inline: auto;
  span {
    display: inline-block;
    &.top {
      color: var(--lime-green);
      position: relative;
      float: right;
      right: 0;
      top: 0;
      animation: moveLeft 1s ease-in-out forwards;
    }

    &.middle {
      width: 100%;
      color: var(--light-green);
      text-align: center;
      transform: rotate(-36deg);
      animation: rotateToNormal 1s ease-in-out forwards;
    }

    &.bottom {
      position: relative;
      color: var(--green);
      text-align: start;
      left: 0;
      top: 0;
      animation: moveRight 1s ease-in-out forwards;
    }
  }
}

@media screen and (min-width: 64rem) {
  h1 {
    margin-block: 4.25rem 3rem;
  }
}

@keyframes moveLeft {
  0% {
    transform: translateX(0);
    right: 0;
  }
  100% {
    transform: translateX(100%);
    right: 100%;
  }
}

@keyframes moveRight {
  0% {
    transform: translateX(0);
    left: 0;
  }
  100% {
    transform: translateX(-100%);
    left: 100%;
  }
}

@keyframes rotateToNormal {
  0% {
    transform: rotate(-36deg);
  }
  100% {
    transform: rotate(0);
  }
}
</style>
