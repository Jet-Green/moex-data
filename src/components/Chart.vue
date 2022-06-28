<script setup>
import { ref } from 'vue'
import { LineChart } from 'vue-chart-3';
import { Chart, registerables } from "chart.js";

Chart.register(...registerables);

let selectedTicker = ref('')
let options = ref(['SBER', 'SBERP', 'NORN'])
const chartData = ref({
    labels: ['Paris', 'Nîmes', 'Toulon', 'Perpignan', 'Autre'],
    datasets: [
        {
            data: [30, 40, 60, 70, 5],
            backgroundColor: ['#77CEFF', '#0079AF', '#123E6B', '#97B0C4', '#A5C8ED'],
        },
    ],
});
const handleChange = value => {
    console.log(`selected ${value}`);
};
</script>
<template>
    <a-typography-title>SBERP</a-typography-title>
    <!-- <a-select v-model:value="selectedTicker" mode="tags" style="width: 100%" placeholder="Tags Mode" :options="options"
        @change="handleChange"></a-select> -->
    <LineChart :chart-data="chartData" />
</template>