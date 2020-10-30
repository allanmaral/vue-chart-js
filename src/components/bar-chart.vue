<template>
  <canvas></canvas>
</template>

<script>
import Chart from "chart.js";

/**
 * Chart serie objet
 * @typedef {Object} GraphSerie
 * @property {string} name - Name of the value being rendered.
 * @property {Array<number>} values - List of values, each entry should be a bar or point.
 * @property {(string | undefined)} color - Optional color of the bar or line.
 */

/**
 * Compose the dataset object used by Chartjs
 * @param {Array<GraphSerie>} series
 */
const createDataset = (series) => {
  return series.map((s) => ({
    label: s.name,
    data: s.values,
    borderColor: s.color || "#027ae3",
    backgroundColor: s.color ? `${s.color}50` : "#027ae360",
    borderWidth: 1,
  }));
};

export default {
  name: "BarChart",
  props: ["labels", "series", "options"],
  data() {
    return {
      chart: null,
    };
  },
  watch: {
    labels() {
      console.log(this.labels);
      this.refresh();
    },
    series() {
      console.log(this.series);
      this.refresh();
    },
  },
  methods: {
    refresh() {
      this.chart.data.labels = this.labels;
      this.chart.data.datasets = createDataset(this.series);
      this.chart.update();
    },
  },
  mounted() {
    this.chart = new Chart(this.$el, {
      type: "bar",
      data: {
        labels: this.labels,
        datasets: createDataset(this.series),
      },
      options: {
        responsive: true,
        scales: {
          yAxes: [
            {
              ticks: {
                beginAtZero: true,
              },
            },
          ],
        },
      },
    });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
