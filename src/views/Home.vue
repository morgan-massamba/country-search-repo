<template>
  <div class="container">
    <Navigation />
    <Wall />
  </div>
</template>

<script>
import Navigation from '@/components/Navigation.vue';
import Wall from '@/components/Wall.vue';

export default {
  name: 'Home',
  components: {
    Wall,
    Navigation,
  },
};
</script>

<style lang="scss" scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Nunito Sans', sans-serif;
}

.container {
  min-height: 100vh;
  width: 100%;
  margin: 0 auto;
}
</style>
