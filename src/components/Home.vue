<template lang="html">
  <div id="home">
    <h1>Trade or View your portfolio</h1>
    <h6>You may Save / Load your Data</h6>
    <h6>Click on 'End Day' to begin a New Day</h6>
    <hr />
    <p><strong>Your Funds:</strong> {{ funds | currency }}</p>
  </div>
</template>

<script>
export default {
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
  },
};
</script>

<style lang="css" scoped>
h1 {
  margin: 50px 0 30px;
}
</style>
