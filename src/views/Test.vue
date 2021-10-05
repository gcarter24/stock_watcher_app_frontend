<template>
  <div class="test">
    <div v-for="stock in series" v-bind:key="stock.id">
      <apexchart width="800" type="bar" :options="options" :series="series"></apexchart>
      Stock Date: {{ stock.date }}
    </div>
  </div>
</template>
<script>
import axios from "axios";
import VueApexCharts from "vue-apexcharts";
import Vue from "vue";
Vue.use(VueApexCharts);
Vue.component("apexchart", VueApexCharts);
export default {
  name: "HelloWorld",
  data: function () {
    return {
      series: [
        {
          name: "series-1",
          data: [],
        },
      ],
      symbol: "",
      close: 0,
      date: "",
      options: {
        chart: {
          id: "vuechart-example",
        },
        xaxis: {
          categories: ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"],
        },
        title: {
          text: "Monthly Stock Pricing",
          align: "center",
          style: {
            fontSize: "20px",
          },
        },
        colors: ["#00897b"],
      },
      // series: [
      //   {
      //     name: "series-1",
      //     data: [],
      //   },
      // ],
    };
  },
  created() {
    // console.log(this.$route.params.id);
    // axios.get(`/api/stocks/${this.$route.params.id}`).then(response => {
    //   console.log(response.data);
    //   this.stock = response.data;
    // });
    this.searchStocks();
  },
  methods: {
    searchStocks() {
      console.log("stock");
      axios
        .get(`/api/stocks/stocks?search=ibm`)
        .then((response) => {
          this.series = [
            {
              data: response.data.close,
            },
          ];
          console.log(response.data);
          // this.stocks = response.data;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>
<style scoped>
div.chart-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
