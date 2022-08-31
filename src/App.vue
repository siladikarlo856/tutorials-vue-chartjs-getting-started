<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <h1>Vite + Vue</h1>
  <button @click="onClickToggleChart">Show/hide chart</button>
  <button @click="onClickChangeData">Change data</button>
  <button @click="onClickChangeLabels">Change labels</button>

  <BarChart
    v-if="isChartVisible"
    :chart-data="chartData"
    :chart-options="chartOptions"
  />
</template>

<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import BarChart from "./components/BarChart.vue";
import { ref } from "vue";

const isChartVisible = ref(true);

const chartData = ref({
  labels: ["January", "February", "March"],
  datasets: [
    {
      label: "Data One",
      backgroundColor: "#f87979",
      data: [40, 20, 12],
    },
  ],
});
const chartOptions = ref({
  responsive: true,
});

function onClickChangeData() {
  chartData.value.datasets[0].data = [20, 30, 0];
}

function onClickChangeLabels() {
  chartData.value.labels = ["Alen", "Karlo", "Ivana"];
}

function onClickToggleChart() {
  isChartVisible.value = !isChartVisible.value;
}
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
