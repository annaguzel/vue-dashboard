<template>
  <div>
    <div class="chart-wrapper">
      <apexchart
        width="800"
        :type="chartType"
        :options="options"
        :series="series"
      >
      </apexchart>
    </div>
  </div>
</template>

<script>
export default {
  name: "SimpleChart",
  props: ["categories", "seriesData", "title", "chartType"],
  data: () => ({
    options: {
      chart: {
        id: "vuechart-example",
      },
      xaxis: {
        categories: [],
      },
      title: {
        text: "",
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
        data: [],
      },
    ],
  }),
  async created() {
    this.options.xaxis.categories = this.categories;
    this.series[0].data = this.seriesData;
    this.options.title.text = this.title;
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
