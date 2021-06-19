<template>
  <div id="app">
    <h1>Vue Apexcharts Demo</h1>
    <div v-for="chart in charts" :key="chart.title">
      <SimpleChart
        v-if="chart.type === 'line' || chart.type === 'bar'"
        :categories="chart.data.categories"
        :seriesData="chart.data.seriesData"
        :title="chart.title"
        :chartType="chart.type"
      />
      <PieChart
        v-else-if="chart.type === 'pie'"
        :categories="chart.data.categories"
        :seriesData="chart.data.seriesData"
        :title="chart.title"
        :chartType="chart.type"
      />
    </div>
  </div>
</template>

<script>
import SimpleChart from "./components/SimpleChart.vue";
import PieChart from "./components/PieChart.vue";

export default {
  name: "App",
  components: {
    SimpleChart,
    PieChart,
  },
  data() {
    return {
      charts: [
        {
          title: "Monthly Stock Pricing",
          type: "line",
          data: {
            categories: [
              "Jan",
              "Feb",
              "Mar",
              "Apr",
              "May",
              "Jun",
              "Jul",
              "Aug",
              "Sep",
              "Oct",
              "Nov",
              "Dec",
            ],

            seriesData: [55, 62, 89, 66, 98, 72, 101, 75, 94, 120, 117, 139],
          },
        },
        {
          title: "Monthly Sales",
          type: "bar",
          data: {
            categories: [
              "Jan",
              "Feb",
              "Mar",
              "Apr",
              "May",
              "Jun",
              "Jul",
              "Aug",
              "Sep",
              "Oct",
              "Nov",
              "Dec",
            ],

            seriesData: [
              1200,
              4500,
              2500,
              1900,
              3400,
              2777,
              5000,
              4100,
              3670,
              1234,
              4200,
              2790,
            ],
          },
        },
        {
          type: "pie",
          title: "Sales by Team",
          data: {
            categories: ["Team A", "Team B", "Team C", "Team D", "Team E"],
            seriesData: [44, 55, 13, 43, 22],
          },
        },
      ],
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
