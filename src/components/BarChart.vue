<template>
  <Bar
    :chart-options="chartOptions"
    :chart-data="chartData"
    :chart-id="chartId"
    :dataset-id-key="datasetIdKey"
    :plugins="plugins"
    :css-classes="cssClasses"
    :styles="styles"
    :width="width"
    :height="height"
    ref="bar"
    @chart:rendered="onChartRendered"
    @chart:destroyed="onChartDestroyed"
    @chart:updated="onChartUpdated"
    @labels:updated="onLabelsUpdated"
  />
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from "vue";
import { Bar } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
} from "chart.js";

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale
);

export default defineComponent({
  name: "BarChart",
  props: {
    chartId: {
      type: String,
      default: "bar-chart",
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
    plugins: {
      type: Object,
      default: () => {},
    },
    chartData: {
      type: Object,
      required: true,
    },
    chartOptions: {
      type: Object,
      default: () => {},
    },
  },
  components: {
    Bar,
  },
  setup(props: any, ctx: any) {
    // declare a ref to hold the element reference
    // the name must match template ref value
    const bar = ref(null);

    function onChartRendered() {
      console.log("chart:rendered");
    }

    function onChartDestroyed() {
      console.log("chart:destroyed");
    }

    function onChartUpdated() {
      console.log("chart:updated");
    }

    function onLabelsUpdated() {
      console.log("labels:updated");
    }

    // on create
    console.log("onCreate", "context: ", ctx, "chart instance", bar.value);

    onMounted(() => {
      console.log("onMounted", "context: ", ctx, "chart instance", bar.value);
    });

    return {
      bar,
      onChartRendered,
      onChartDestroyed,
      onChartUpdated,
      onLabelsUpdated,
    };
  },
});
</script>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
