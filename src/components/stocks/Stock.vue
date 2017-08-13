<template lang="html">
  <div class="stock col-md-6 col-lg-4">
    <div class="card bg-light">
      <div class="card-header"><strong>{{ stock.name }}</strong> (Price: {{ stock.price }})</div>
      <div class="card-body">
        <div class="input-group">
          <input
            type="numner"
            class="form-control"
            placeholder="Quantity..."
            aria-label="Quantity..."
            v-model="quantity"
          />
          <span class="input-group-btn">
            <button
              class="btn btn-success"
              type="button"
              @click="buyStock"
              :disabled="quantity <= 0 || Number.isNaN(Number(quantity))"
            >Buy</button>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['stock'],
  data() {
    return {
      quantity: null,
    };
  },
  methods: {
    buyStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity,
      };
      this.$store.dispatch('buyStock', order);
      this.quantity = null;
    },
  },
};
</script>

<style lang="css" scoped>
.stock {
  margin-bottom: 30px;
}
</style>
