<template lang="html">
  <div id="navbar">
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">
        <router-link to="/" class="navbar-brand">Stock Trader</router-link>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav mr-auto">
            <router-link to="/" exact class="nav-item" activeClass="active" tag="li"><a class="nav-link">Home</a></router-link>
            <router-link to="/stocks" class="nav-item" activeClass="active" tag="li"><a class="nav-link">Stocks</a></router-link>
            <router-link to="/portfolio" class="nav-item" activeClass="active" tag="li"><a class="nav-link">Portfolio</a></router-link>
          </ul>
          <span class="navbar-text">
            <strong>Funds:</strong> {{ funds | currency }}
          </span>
          <ul class="navbar-nav my-2 my-lg-0">
            <li class="nav-item dropdown" :class="{show: isDropdownOpen}">
              <a class="nav-link dropdown-toggle" id="navbarDropdownMenuLink" data-toggle="dropdown" aria-haspopup="true" @click="isDropdownOpen = !isDropdownOpen">Save / Load</a>
              <div class="dropdown-menu" :class="{show: isDropdownOpen}" aria-labelledby="navbarDropdownMenuLink">
                <a class="dropdown-item" href="#" @click="saveData">Save Data</a>
                <a class="dropdown-item" href="#" @click="loadData">Load Data</a>
              </div>
            </li>
            <li class="nav-item">
              <button class="btn btn-outline-light btn-end" @click="endDay">End Day</button>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
import { mapActions } from 'vuex';

export default {
  data() {
    return {
      isDropdownOpen: false,
    };
  },
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
  },
  methods: {
    ...mapActions({
      randomizeStocks: 'randomizeStocks',
      fetchData: 'loadData',
    }),
    endDay() {
      this.randomizeStocks();
    },
    saveData() {
      const data = {
        funds: this.$store.getters.funds,
        stockPortfolio: this.$store.getters.stockPortfolio,
        stocks: this.$store.getters.stocks,
      };
      this.$http.put('data.json', data);
    },
    loadData() {
      this.fetchData();
    },
  },
};
</script>

<style lang="css" scoped>
#navbar {
  margin-bottom: 1.5rem;
}
.navbar-text {
  color: #fff;
  margin-right: 30px;
}
.btn-end {
  margin-left: 30px;
}
.btn-end:hover {
  color: #343a40;
}
.dropdown-toggle, .btn-end {
  cursor: pointer;
}
</style>
