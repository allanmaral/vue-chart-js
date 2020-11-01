<template>
  <canvas />
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
  // Retrive the primary color to be used as default
  const defaultBgColor = getComputedStyle(
    document.documentElement
  ).getPropertyValue("--q-color-primary");
  const defaultBorderColor = `${defaultBgColor}50`;

  return series.map((s) => ({
    label: s.name,
    data: s.values,
    borderColor: s.color || defaultBgColor,
    backgroundColor: s.color ? `${s.color}50` : defaultBorderColor,
    borderWidth: 1,
  }));
};

export default {
  name: "BarChart",
  props: {
    labels: {
      type: Array,
      required: true,
    },
    series: {
      type: Array,
      required: true,
    },
    horizontal: {
      type: Boolean,
      required: false,
      default: false,
    },
    title: {
      type: String,
      rendered: false,
      default: null,
    },
    xUnit: {
      type: String,
      required: false,
      default: "",
    },
    yUnit: {
      type: String,
      required: false,
      default: "",
    },
  },
  data() {
    return {
      chart: null,
    };
  },
  watch: {
    labels() {
      this.updateChart();
    },
    series() {
      this.updateChart();
    },
    options() {
      this.updateChart();
    },
  },
  methods: {
    updateChart() {
      this.chart.data.labels = this.labels;
      this.chart.data.datasets = createDataset(this.series);
      this.chart.update();
    },
  },
  mounted() {
    this.chart = new Chart(this.$el, {
      type: this.horizontal ? "horizontalBar" : "bar",
      data: {
        labels: this.labels,
        datasets: createDataset(this.series),
      },
      options: {
        responsive: true,
        title: {
          display: !!this.title,
          text: this.title,
        },
        scales: {
          yAxes: [
            {
              ticks: {
                beginAtZero: true,
                callback: (value) => {
                  return `${value}${this.yUnit}`;
                },
              },
            },
          ],
          xAxes: [
            {
              ticks: {
                beginAtZero: true,
                callback: (value) => {
                  return `${value}${this.xUnit}`;
                },
              },
            },
          ],
        },
        ...this.options,
      },
    });
  },
};
</script>

<style scoped>
</style>
