<template>
  <div class="about">
    <h1>Chart Test Page</h1>
  </div>
</template>
<style></style>
<script>
import axios from "axios";
import ApexCharts from "apexcharts";
export default {
  name: "HelloWorld",
  data: () => ({
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
    series: [
      {
        name: "series-1",
        data: [55, 62, 89, 66, 98, 72, 101, 75, 94, 120, 117, 139],
      },
    ],
  }),
  created: function () {
    var chart = new ApexCharts(document.querySelector("#chart"));
    var url = "https://cloud.iexapis.com/stable/stock/IBM/chart/30d?token=sk_f6971a8e7d174aac9d0283a79d9b7d45";

    axios({
      method: "GET",
      url: url,
    }).then(function (response) {
      chart.updateSeries([
        {
          name: "Sales",
          data: response.data,
        },
      ]);
    });
  },
};
</script>
