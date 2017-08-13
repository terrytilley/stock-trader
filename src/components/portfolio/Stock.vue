<template lang="html">
  <div class="stock col-md-6 col-lg-4">
    <div class="card bg-light">
      <div class="card-header"><strong>{{ stock.name }}</strong> (Price: {{ stock.price }}) | (Quantity: {{ stock.quantity }})</div>
      <div class="card-body">
        <div class="input-group">
          <input
            type="numner"
            class="form-control"
            :class="{'is-invalid': insufficientQuantity}"
            placeholder="Quantity..."
            aria-label="Quantity..."
            v-model="quantity"
          />
          <span class="input-group-btn">
            <button
              class="btn btn-danger"
              type="button"
              @click="sellStock"
              :disabled="insufficientQuantity || quantity <= 0 || Number.isNaN(Number(quantity))"
            >{{ insufficientQuantity ? 'Not Enough Stocks' : 'Sell' }}</button>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex';

export default {
  props: ['stock'],
  data() {
    return {
      quantity: null,
    };
  },
  computed: {
    insufficientQuantity() {
      return this.quantity > this.stock.quantity;
    },
  },
  methods: {
    ...mapActions({
      placeSellOrder: 'sellStock',
    }),
    sellStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity,
      };
      this.placeSellOrder(order);
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
