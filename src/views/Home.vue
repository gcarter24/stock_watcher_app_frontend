<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <input type="text" v-model="search" placeholder="Search Stocks" />
    <div v-for="stock in filteredStocks" v-bind:key="stock.id">
      <p>Name: {{ stock.name }}</p>
      <p>Symbol: {{ stock.symbol }}</p>
      <hr />
    </div>
    <!-- <button v-on:click="filteredStocks()">Search</button> -->
    <!-- <p>{{ stock.name }}</p> -->
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      id: "",
      symbol: "",
      name: "",
      search: "",
      stocks: [],
    };
  },
  created: function () {
    axios.get(`/api/stocks/`).then((response) => {
      console.log(response.data);
      this.stocks = response.data;
    });
    // this.filteredStocks();
  },
  methods: {
    // searchStocks: function () {
    // var params = { symbol: this.symbol, name: this.name, id: this.id };
    // axios.get(`/api/stocks/`).then((response) => {
    //   console.log(response.data);
    //   this.stocks = response.data;
    // });
    // },
  },
  computed: {
    filteredStocks: function () {
      return this.stocks.filter((stock) => {
        return (
          stock.name.toLowerCase().match(this.search.toLowerCase()) ||
          stock.symbol.toLowerCase().match(this.search.toLowerCase())
        );
      });
    },
  },
};
</script>
