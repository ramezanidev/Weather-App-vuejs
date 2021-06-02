<template>
  <div>
    <canvas
      style="display: block; width: 794px; height: 255px"
      width="794"
      height="255"
      ref="Chart"
      class="chartjs-render-monitor"
    ></canvas>
  </div>
</template>

<script>
import Chart from 'chart.js'
export default {
  name: "chart",
  props: ["tempList", "dateList"],
  watch: {
    tempList: function () {
      this.setChart();
    },
  },
  methods: {
    setChart: function () {
      let el = this.$refs.Chart.getContext("2d");
      new Chart(el, {
        type: "line",
        data: {
          labels: this.dateList,
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
              data: this.tempList,
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
    },
  },
};
</script>

<style>
canvas {
    width: 100% !important;
    height: 255px !important;
}
</style>