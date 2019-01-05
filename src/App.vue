<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style lang="scss">
  * {
    box-sizing: border-box;
  }

  body, html {
    margin: 0;
    padding: 0;
    font-size: 10px;
  }

  .content {
    max-width: 1400px;
    margin: auto;
  }
</style>
