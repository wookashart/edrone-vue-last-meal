<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style lang="scss">
  @import './styles/colors';

  * {
    box-sizing: border-box;
  }

  body, html {
    margin: 0;
    padding: 0;
    font-size: 10px;
  }

  h3 {
    font-size: 2.2rem;
    margin: 0;
  }

  .content {
    max-width: 1400px;
    margin: auto;
  }

  .information {
    width: 100%;
    border: 1px solid $gray;
    margin: 0 20px;
    border-radius: 10px;
    overflow: hidden;
  }
</style>
