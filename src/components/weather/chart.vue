<template>
  <div>
    <canvas
      style="display: block; width: 794px; height: 255px"
      width="794"
      height="255"
      ref="canvas"
      class="chartjs-render-monitor"
    ></canvas>
  </div>
</template>

<script setup>
import { defineProps, watch, ref, computed } from "vue";

import Chart from "chart.js";
console.log(Chart)
const props = defineProps({
  tempList: {
    type: Array,
    default: () => ([])
  },
  dateList: {
    type: Array,
    default: () => ([])
  },
});

const canvas = ref(null);

const setChart = () => {
  if (canvas.value) {
    let el = canvas.value.getContext("2d");
    new Chart(el, {
      type: "line",
      data: {
        labels: props.dateList,
        datasets: [
          {
            label: "Data",
            borderColor: "#ccc",
            pointBorderColor: "#fff",
            pointHoverBackgroundColor: "#008bff",
            pointBorderWidth: 8,
            pointHoverRadius: 10,
            pointHoverBorderWidth: 1,
            pointRadius: 2,
            fill: !0,
            borderWidth: 1,
            data: props.tempList,
          },
        ],
      },
      options: {
        tooltips: {
          callbacks: {
            label: function (e) {
              return e.yLabel;
            },
          },
        },
        legend: { display: false },
        responsive: true,
        maintainAspectRatio: false,
        scales: {
          yAxes: [
            {
              ticks: {
                fontColor: "#ccc",
                fontStyle: "lighter",
                beginAtZero: true,
                maxTicksLimit: 5,
                padding: 15,
              },
              gridLines: { drawTicks: true, display: true },
            },
          ],
          xAxes: [
            {
              gridLines: { zeroLineColor: "transparent" },
              ticks: {
                padding: 15,
                fontColor: "#ccc",
                fontStyle: "lighter",
              },
            },
          ],
        },
      },
    });
  }
};
const data = computed(() => props.tempList)
watch(data, setChart);
</script>

<style>
canvas {
  width: 100% !important;
  height: 255px !important;
}
</style>
