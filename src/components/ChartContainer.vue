<template>
  <div class="container">
    <line-chart v-if="loaded" :chartdata="chartdata" :options="options" />
  </div>
</template>

<script>
//import axios from "axios";
import LineChart from "./Chart.vue";

export default {
  name: "LineChartContainer",
  components: { LineChart },
  data: () => ({
    loaded: false,
    chartdata: null,
  }),
  async mounted() {
    this.loaded = false;
    this.chartdata = {
      labels: ["January", "February"],
      datasets: [
        {
          label: "Data One",
          backgroundColor: "#f87979",
          data: [40, 20],
        },
      ],
    };
    this.options = {
      responsive: true,
      maintainAspectRatio: false,
    };
  },
};
</script>
