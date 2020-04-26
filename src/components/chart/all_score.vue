<template>
  <div style="width: 100%; height: 100%; background-color: #fff;">
    <div style="height: 100%; width: 100%;">
      <div id="all_score" style="width:100%; height:620px;"></div>
    </div>
  </div>
</template>


<script>
import echarts from "echarts";
import axios from "axios";

export default {
  name: "all_score",
  props: ["jsonData_score"],
  data() {
    return {
      score: this.jsonData_score.score,
      name: this.jsonData_score.name
    };
  },
  mounted() {
    // this.getSource();
    this.getChart();
  },
  methods: {
    // getSource() {
    //   axios.get("http://127.0.0.1:8000/score/").then(response => {
    //     this.score = response.data.score;
    //     this.name = response.data.name;
    //     this.getChart();
    //     // console.log(typeof this.bookinfo);
    //     // console.log(response.data);
    //   });
    // },
    getChart() {
      var myChart = echarts.init(document.getElementById("all_score"));
      var option = {
        tittle: {
          text: this.name + "总评分",
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
            detail: { formatter: "豆瓣评分：{value}分" },
            data: [{ value: 10 * this.score, name: this.name + "总评分" }]
          }
        ]
      };
      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
    }
  }
};
</script>