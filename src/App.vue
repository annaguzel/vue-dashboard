<template>
  <div id="app" class="flex">
    <h1 class="w-full">Vue Dynamic Dashboard</h1>
    <div
      v-for="chart in charts"
      :key="chart.title"
      :class="'chart-container w-' + chart.size"
    >
      <div v-if="chart.data">
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
        <Table
          v-else-if="chart.type === 'table'"
          :contents="chart.data.contents"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SimpleChart from "./components/SimpleChart.vue";
import PieChart from "./components/PieChart.vue";
import Table from "./components/Table.vue";
export default {
  name: "App",

  components: {
    SimpleChart,
    PieChart,
    Table,
  },
  created() {
    this.getMeta();
  },
  data() {
    return {
      charts: null,
      getDataIndex: 0,
    };
  },
  methods: {
    getMeta() {
      this.$http.get("https://demo1368642.mockable.io/charts/").then((res) => {
        this.charts = res.data.sort((a, b) => (a.order > b.order ? 1 : -1));
        const orderedIds = res.data
          .sort((a, b) => (a.priority > b.priority ? 1 : -1))
          .map((item) => item.id);
        this.getData(orderedIds);
      });
    },
    getData(ids) {
      if (this.getDataIndex < this.charts.length) {
        this.$http
          .get(
            `http://demo1368642.mockable.io/charts/${ids[this.getDataIndex]}/`
          )
          .then((res) => {
            this.charts = this.charts.map((item) => {
              if (item.id === ids[this.getDataIndex]) {
                item.data = res.data;
              }
              return item;
            });
            this.getDataIndex++;
            this.getData(ids);
          });
      }
    },
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
.flex {
  display: flex;
  flex-wrap: wrap;
}
.w-full {
  width: 100%;
}
.w-2\/3 {
  width: 66.666%;
}
.w-1\/3 {
  width: 33.333%;
}
.w-1\/2 {
  width: 50%;
}
.chart-container {
  padding: 5em;
  align-self: center;
}
</style>
