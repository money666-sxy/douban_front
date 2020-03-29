<template>
  <div style="width: 100%; height: 100%; background-color: #fff;">
    <div style="height: 100%; width: 100%;">
      <div id="all_score" style="width:100%; height:620px;"></div>
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
      var myChart = echarts.init(document.getElementById("all_score"));
      var option = {
        tittle: {
          text: "某图书总评分",
          subtext: "仪表盘",
          left: "center"
        },
        tooltip: {
          formatter: "{a} <br/>{b} : {c}%"
        },
        toolbox: {
          feature: {
            restore: {},
            saveAsImage: {}
          }
        },
        series: [
          {
            name: "总评分",
            type: "gauge",
            detail: { formatter: "{value}%" },
            data: [{ value: 66, name: "总评分" }]
          }
        ]
      };
      myChart.setOption(option);
    }
  }
};
</script>