<template>
  <div id="app">
    <div>
      <button @click="addData">Add data</button>
      <button @click="removeData">Remove data</button>
      <button @click="randomize">Regenerate</button>
    </div>
    <bar-chart :labels="labels" :series="series" />
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
          name: "# por área",
          color: "#027ae3",
          values: [12, 19, 3, 5, 2],
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
        serie.values = s.values.map(() => Math.floor(Math.random() * 20));
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
