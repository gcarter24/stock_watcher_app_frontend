<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="stock in stocks" v-bind:key="stock.id">
      <p>Name: {{ stock.name }}</p>
      <p>Symbol: {{ stock.symbol }}</p>
      <hr />
    </div>
    <button v-on:click="searchStock()">Search</button>
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
      stocks: {},
    };
  },
  created: function () {},
  methods: {
    searchStock: function () {
      // var params = { symbol: this.symbol, name: this.name, id: this.id };
      axios.get("/api/stocks/").then((response) => {
        console.log(response.data);
        this.stocks = response.data;
      });
    },
  },
};
</script>
