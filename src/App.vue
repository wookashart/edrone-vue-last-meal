<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style lang="scss">
  @import './styles/colors';
  @import './styles/mixins';

  * {
    box-sizing: border-box;
    font-family: 'Open Sans', sans-serif;
  }

  body,
  html {
    margin: 0;
    padding: 0;
    font-size: 10px;
  }

  h3 {
    font-size: 2rem;
    margin: 0;
  }

  p,
  li {
    font-size: 1.2rem;
  }

  .content {
    max-width: 1400px;
    margin: auto;
  }
</style>
