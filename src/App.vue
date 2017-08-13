<template>
  <div id="app">
    <Navbar />
    <div class="container">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar';

export default {
  name: 'app',
  components: {
    Navbar,
  },
  created() {
    this.$store.dispatch('initStocks');
  },
};
</script>

<style lang="css" scoped>
</style>
