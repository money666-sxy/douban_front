<template>
  <div style="width: 100%; height: 100%; background-color: #fff;">
    <div style="height: 100%; width: 100%;">
      <div id="heatmap" style="width:100%; height:620px;">
        <!-- <img src="douban_front/src/assets/chart_heatmap.png" alt="时间热力图" /> -->
      </div>
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
      var myChart = echarts.init(document.getElementById("heatmap"));
      var hours = ;
      var days = ;

      var data = ;

      data = data.map(function(item) {
        return [item[1], item[0], item[2] || "-"];
      });
      var option = {
        title: {
          text: "某图书评论时间分析图",
          subtext: "热力图图",
          left: "center"
        },
        tooltip: {
          position: "top"
        },
        animation: false,
        grid: {
          height: "50%",
          top: "10%"
        },
        xAxis: {
          type: "category",
          data: hours,
          splitArea: {
            show: true
          }
        },
        yAxis: {
          type: "category",
          data: days,
          splitArea: {
            show: true
          }
        },
        visualMap: {
          min: 0,
          max: 10,
          calculable: true,
          orient: "horizontal",
          left: "center",
          bottom: "15%"
        },
        series: [
          {
            name: "Punch Card",
            type: "heatmap",
            data: data,
            label: {
              show: true
            },
            emphasis: {
              itemStyle: {
                shadowBlur: 10,
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


<script>
import echarts from "echarts";
import axios from "axios";

export default {
  name: "all_score",
  props: ["jsonData_heat"],
  data() {
    return {
      year: this.jsonData_heat.year_list,
      months: this.jsonData_heat.mon_list,
      ymn_data: this.jsonData_heat.ym_num_list,
      name: this.jsonData_heat.name
    };
  },
  mounted() {
    // this.getSource();
    this.getChart();
  },
  methods: {
    // getSource() {
    //   axios.get("http://127.0.0.1:8000/time/").then(response => {
    //     this.year = response.data.year_list;
    //     this.month = response.data.mon_list;
    //     this.ymn_data = response.data.ym_num_list;

    //     this.name = response.data.name;
    //     this.getChart();
    //     // console.log(typeof this.bookinfo);
    //     // console.log(response.data);
    //   });
    // },
    getChart() {
      var myChart = echarts.init(document.getElementById("heatmap"));
      var years = this.year;
      var months = this.months;

      var data = this.ymn_data;

      data = data.map(function(item) {
        return [item[1], item[0], item[2] || "-"];
      });
      var option = {
        title: {
          text: this.name + "评论数量（年/月）热力图",
          subtext: "某一时间评论数量",
          left: "center"
        },
        tooltip: {
          position: "top"
        },
        animation: false,
        grid: {
          height: "50%",
          top: "10%"
        },
        xAxis: {
          type: "category",
          name: "月份",
          data: months,
          splitArea: {
            show: true
          }
        },
        yAxis: {
          type: "category",
          name: "年份",
          data: years,
          splitArea: {
            show: true
          }
        },
        visualMap: {
          min: 0,
          max: 10,
          calculable: true,
          orient: "horizontal",
          left: "center",
          bottom: "15%"
        },
        series: [
          {
            name: "Punch Card",
            type: "heatmap",
            data: data,
            label: {
              show: true
            },
            emphasis: {
              itemStyle: {
                shadowBlur: 10,
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