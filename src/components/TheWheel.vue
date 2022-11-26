<template>
  <Pie
    :chart-options="chartOptions"
    :chart-data="chartData"
    :chart-id="chartId"
    :dataset-id-key="datasetIdKey"
    :plugins="plugins"
    :css-classes="cssClasses"
    :styles="styles"
    :width="width"
    :height="height"
    ref="wheel"
  />
</template>

<script>
import { Pie } from "vue-chartjs";
import { Chart as ChartJS, Title, ArcElement } from "chart.js";
import ChartDataLabels from "chartjs-plugin-datalabels";

ChartJS.register(Title, ArcElement);

export default {
  components: { Pie },
  props: {
    chartId: {
      type: String,
      default: "pie-chart",
    },
    labelProp: {
      required: true,
    },
    datasetIdKey: {
      type: String,
      default: "label",
    },
    width: {
      type: Number,
      default: 400,
    },
    height: {
      type: Number,
      default: 400,
    },
    cssClasses: {
      default: "",
      type: String,
    },
    styles: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {
      plugins: [ChartDataLabels],
    };
  },
  computed: {
    chartData() {
      return {
        labels: this.labelProp,
        datasets: [
          {
            backgroundColor: ["#1976d2", "#1e88e5"],
            data: this.labelProp.map((e) => 1),
          },
        ],
      };
    },
    chartOptions() {
      return {
        animation: { duration: 0 },
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          datalabels: {
            color: "#ffffff",
            formatter: (_, context) =>
              context.chart.data.labels[context.dataIndex],
            font: { size: 16 },
          },
        },
      };
    },
  },
};
</script>
