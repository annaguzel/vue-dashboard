<template>
  <div>
    <div class="chart-wrapper">
      <apexchart
        type="pie"
        width="380"
        :options="chartOptions"
        :series="series"
      ></apexchart>
    </div>
  </div>
</template>

<script>
export default {
  name: "PieChart",
  props: ["categories", "seriesData", "title", "chartType"],
  data: () => ({
    series: [],
    chartOptions: {
      chart: {
        width: 380,
        type: "pie",
      },
      labels: [],
      responsive: [
        {
          breakpoint: 480,
          options: {
            chart: {
              width: 200,
            },
            legend: {
              position: "bottom",
            },
          },
        },
      ],
    },
  }),
  async created() {
    this.chartOptions.labels = this.categories;
    this.series = this.seriesData;
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
