<template>
  <h1>
    <span class="top">WE'RE</span>
    <span class="middle">COMING</span>
    <span class="bottom">SOON</span>
  </h1>
</template>

<style lang="scss" scoped>
h1 {
  font-family: "Nico Moji", sans-serif;
  font-size: 3rem;
  line-height: 1.5;
  span {
    display: inline-block;
    &.top {
      color: var(--lime-green);
      position: relative;
      float: right;
      right: 0;
      top: 0;
    }

    &.middle {
      display: block;
      color: var(--light-green);
      text-align: center;
      transform: rotate(-36deg);
    }

    &.bottom {
      color: var(--green);
      text-align: start;
      left: 0;
      top: 0;
    }
  }
}
</style>
