
<template>
  <div style="width: 100%; height: 100%; background-color: #fff;">
    <div style="height: 100%; width: 100%;">
      <div id="star_hist" style="width:100%; height:620px;"></div>
    </div>
  </div>
</template>




<script>
import echarts from "echarts";
import axios from "axios";

export default {
  name: "all_score",
  props: ["jsonData_star"],
  data() {
    return {
      name: this.jsonData_star.name,
      five_star: this.jsonData_star.five_star,
      four_star: this.jsonData_star.four_star,
      three_star: this.jsonData_star.three_star,
      two_star: this.jsonData_star.two_star,
      one_star: this.jsonData_star.one_star
    };
  },
  mounted() {
    // this.getSource();
    this.getChart();
  },
  methods: {
    // getSource() {
    //   axios.get("http://127.0.0.1:8000/star/").then(response => {
    //     this.name = response.data.name;
    //     this.five_star = response.data.five_star;
    //     this.four_star = response.data.four_star;
    //     this.three_star = response.data.three_star;
    //     this.two_star = response.data.two_star;
    //     this.one_star = response.data.one_star;

    //     this.getChart();
    //     // console.log(typeof this.bookinfo);
    //     // console.log(response.data);
    //   });
    // },
    getChart() {
      var myChart = echarts.init(document.getElementById("star_hist"));
      var option = {
        title: {
          text: this.name + "星级评分",
          // text: jsonData_star.name + "星级评分",
          subtext: "柱状图",
          left: "center"
        },
        xAxis: {
          type: "category",
          name: "星级分布",
          data: ["五星", "四星", "三星", "二星", "一星"]
        },
        yAxis: {
          type: "value",
          name: "星级所占百分比"
        },
        series: [
          {
            data: [
              this.five_star,
              this.four_star,
              this.three_star,
              this.two_star,
              this.one_star
            ],
            type: "bar",
            showBackground: true,
            backgroundStyle: {
              color: "rgba(220, 220, 220, 0.8)"
            }
          }
        ]
      };
      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
    }
  }
};
</script>