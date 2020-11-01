<template>
  <div id="app">
    <div>
      <button @click="addData">Add data</button>
      <button @click="removeData">Remove data</button>
      <button @click="randomize">Randomize Data</button>
    </div>
    <bar-chart :labels="labels" :series="series" yUnit="%" title="teste" />
  </div>
</template>

<script>
import BarChart from "./components/bar-chart";

export default {
  name: "App",
  components: {
    BarChart,
  },
  data() {
    return {
      title: "Chart.js Bar Chart",
      labels: ["Dorime", "Interino", "Adapare", "Ameno", "Latire"],
      series: [
        {
          name: "Lorem",
          color: "#027ae3",
          values: Array(5)
            .fill(0)
            .map(() => Math.ceil(Math.random() * 20)),
        },
        {
          name: "Ipsum",
          color: "#007E7A",
          values: Array(5)
            .fill(0)
            .map(() => Math.ceil(Math.random() * 20)),
        },
      ],
    };
  },
  methods: {
    addData() {
      this.labels.push(
        [
          "Dorime",
          "Interino",
          "Adapare",
          "Ameno",
          "Latire",
          "Latiremo",
          "Omenare",
          "Imperavi",
          "Dimere",
          "Mantiro",
        ][Math.floor(Math.random() * 10)]
      );
      this.series.forEach((s) => {
        s.values.push(Math.floor(Math.random() * 20));
      });
    },
    removeData() {
      this.labels.pop();
      this.series.forEach((s) => {
        s.values.pop();
      });
    },
    randomize() {
      this.series = this.series.map((s) => {
        const serie = { ...s };
        const values = s.values.map(() => Math.ceil(1 + Math.random() * 19));
        const scale = 100 / values.reduce((sum, cur) => sum + cur, 0);
        serie.values = values.map((v) => v * scale);
        return serie;
      });
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
