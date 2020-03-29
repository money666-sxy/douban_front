
<template>
  <div style="width: 100%; height: 100%; background-color: #fff;">
    <div style="height: 100%; width: 100%;">
      <div id="star_hist" style="width:100%; height:620px;"></div>
    </div>
  </div>
</template>



<script>
import echarts from "echarts";

export default {
  mounted() {
    this.getChart();
  },
  methods: {
    getChart() {
      var myChart = echarts.init(document.getElementById("star_hist"));
      var option = {
        title: {
          text: "某图书星级评分",
          subtext: "柱状图",
          left: "center"
        },
        xAxis: {
          type: "category",
          data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
        },
        yAxis: {
          type: "value"
        },
        series: [
          {
            data: [120, 200, 150, 80, 70, 110, 130],
            type: "bar",
            showBackground: true,
            backgroundStyle: {
              color: "rgba(220, 220, 220, 0.8)"
            }
          }
        ]
      };
      myChart.setOption(option);
    }
  }
};
</script>