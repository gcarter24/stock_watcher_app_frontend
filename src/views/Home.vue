<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <input type="text" v-model="search" placeholder="Search Stocks" />
    <div v-for="stock in filteredStocks" v-bind:key="stock.id">
      <p>Name: {{ stock.name }}</p>
      <p>NASDAQ Symbol: {{ stock.symbol }}</p>
      <p><button v-on:click="stocksShow(stock)">View History</button></p>
      <hr />
    </div>
    <dialog id="stock-details">
      <form method="dialog">
        <p>Name: {{ currentStock.name }}</p>
        <p>Symbol: {{ currentStock.symbol }}</p>
        <p>Industry: {{ currentStock.industry }}</p>
        <p>Sector: {{ currentStock.sector }}</p>
        <p>IPO Year: {{ currentStock.ipo_year }}</p>
        <p>Country: {{ currentStock.country }}</p>
        <button>Close</button>
      </form>
    </dialog>
    <!-- <button v-on:click="filteredStocks()">Search</button> -->
    <!-- <p>{{ stock.name }}</p> -->
  </div>
</template>

<style></style>

<script>
import axios from "axios";
// import ApexCharts from "apexcharts";
export default {
  data: function () {
    return {
      message: "NASDAQ Stock Market Watcher",
      id: "",
      symbol: "",
      name: "",
      search: "",
      stocks: [],
      currentStock: {},
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
    stocksShow: function (theStock) {
      console.log(theStock);
      this.currentStock = theStock;
      document.querySelector("#stock-details").showModal();
    },
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
