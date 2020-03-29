<template>
  <div style="width: 100%; height: 100%; background-color: #fff;">
    <div style="height: 100%; width: 100%;">
      <div id="wordpesg_rose" style="width:100%; height:620px;"></div>
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
      var myChart = echarts.init(document.getElementById("wordpesg_rose"));
      var option = {
        title: {
          text: "某图书词性分析图",
          subtext: "扇形图",
          left: "center"
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
          orient: "vertical",
          left: "left",
          data: ["名词", "动词", "形容词", "副词", "代词"]
        },
        series: [
          {
            name: "访问来源",
            type: "pie",
            radius: "55%",
            center: ["50%", "60%"],
            data: [
              { value: 335, name: "名词" },
              { value: 310, name: "动词" },
              { value: 234, name: "形容词" },
              { value: 135, name: "副词" },
              { value: 1548, name: "代词" }
            ],
            emphasis: {
              itemStyle: {
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowColor: "rgba(0, 0, 0, 0.5)"
              }
            }
          }
        ]
      };
      myChart.setOption(option);
    }
  }
};
</script>