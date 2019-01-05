<template>
  <div class="home">
    <Navigation />
    <div class="content main-box">
      <Aside />
      <Content />
    </div>
  </div>
</template>

<script>
import Navigation from '@/components/Navigation';
import Aside from '@/components/Aside';
import Content from '@/components/Content';

export default {
  name: 'home',
  components: {
    Navigation,
    Aside,
    Content,
  },
};
</script>

<style lang="scss" scoped>
  .main-box {
    display: flex;
  }
</style>
