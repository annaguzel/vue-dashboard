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
    <hr />
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
    this.chartOptions.labels = this.$props.categories;
    this.series = this.$props.seriesData;
    this.options.title.text = this.$props.title;
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
