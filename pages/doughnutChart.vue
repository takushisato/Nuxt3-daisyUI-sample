<script setup lang="ts">
import { Chart as ChartJS, ArcElement, Tooltip, Title, Legend } from "chart.js";
import { Doughnut } from "vue-chartjs";
ChartJS.register(ArcElement, Tooltip, Title, Legend);

// チャート用のデータ
const data = {
  labels: ["Red", "Blue", "Yellow"],
  datasets: [
    {
      data: [80, 15, 5],
      backgroundColor: ["rgb(255, 99, 132)", "rgb(54, 162, 235)", "rgb(255, 205, 86)"],
    },
  ],
};

// チャート描画のオプション
const options = {
  responsive: true,
  maintainAspectRatio: false,
  plugins: {
    title: {
      display: true,
      text: "Doughnut Chart",
      font: {
        weight: "bold",
        size: 40,
      },
    },
    legend: {
      display: true,
      position: "bottom",
      reverse: true,
      labels: {
        font: {
          size: 20,
        },
      },
    },
  },
};

const ratioText = {
  id: "ratio-text",
  beforeDraw(chart: any) {
    const {
      ctx,
      chartArea: { top, width, height },
    } = chart;
    ctx.save();
    //チャート描画部分の中央を指定
    ctx.fillRect(width / 2, top + height / 2, 0, 0);
    //フォントのスタイル指定
    ctx.font = "bold 50px Roboto";
    ctx.fillStyle = "#333333";
    ctx.textAlign = "center";
    ctx.textBaseline = "middle";
    //80%という文字列をドーナツチャートの中央部に描画します
    ctx.fillText("80 %", width / 2, top + height / 2);
  },
};
</script>
<template>
  <div>
    <div class="doughnut-graph">
      <!-- ドーナツチャートの描画 -->
      <Doughnut :data="data" :options="options" :plugins="[ratioText]" />
    </div>
  </div>
</template>
<style>
.doughnut-graph {
  width: 600px;
  height: 600px;
}
</style>
