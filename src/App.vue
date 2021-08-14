<template>
  <div class="container">
    <h1 class="text-center">Coins List</h1>
    <input
      type="text"
      class="form-control mb-4 bg-dark text-light"
      @keyup="filterCoin"
      placeholder="Search Coin"
      v-model="textFilter"
    />
    <Table :coinsFilter="coinsFilter" />
  </div>
</template>

<script>
import Table from "./components/Table.vue";
export default {
  name: "App",
  data() {
    return {
      coins: [],
      coinsFilter: [],
      titles: ["#", "Coin", "Price", "Price Change", "24h Volume"],
      textFilter: "",
    };
  },
  components: {
    Table: Table,
  },
  methods: {
    filterCoin() {
      this.coinsFilter = this.coins.filter(
        (c) =>
          c.name.toLowerCase().includes(this.textFilter.toLowerCase()) ||
          c.symbol.toLowerCase().includes(this.textFilter.toLowerCase())
      );
    },
  },
  async mounted() {
    const res = await fetch(
      "https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false"
    );
    const data = await res.json();
    this.coins = data;
    this.coinsFilter = data;
  },
};
</script>

<style>
body {
  background: #222;
  color: #fff;
}
</style>
