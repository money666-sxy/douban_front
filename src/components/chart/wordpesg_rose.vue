<template>
  <div style="width: 100%; height: 100%; background-color: #fff;">
    <div style="height: 100%; width: 100%;">
      <div id="wordpesg_rose" style="width:100%; height:620px;"></div>
    </div>
  </div>
</template>




<script>
import echarts from "echarts";
import axios from "axios";

export default {
  name: "all_score",
  props: ["jsonData_pesg"],
  data() {
    return {
      pesg_list: this.jsonData_pesg.pesg_list,
      pesg_name: this.jsonData_pesg.pesg_name,
      name: this.jsonData_pesg.name
    };
  },
  mounted() {
    // this.getSource();
    this.getChart();
  },
  methods: {
    // getSource() {
    //   axios.get("http://127.0.0.1:8000/pesg/").then(response => {
    //     this.pesg_list = response.data.pesg_list;
    //     this.pesg_name = response.data.pesg_name;

    //     this.name = response.data.name;
    //     this.getChart();
    //     // console.log(typeof this.bookinfo);
    //     // console.log(response.data);
    //   });
    // },
    getChart() {
      var myChart = echarts.init(document.getElementById("wordpesg_rose"));
      var option = {
        title: {
          text: this.name + "词性分析图",
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
          data: this.pesg_name
          // ["名词", "动词", "形容词", "副词", "代词"]
        },
        series: [
          {
            name: "访问来源",
            type: "pie",
            radius: "55%",
            center: ["50%", "60%"],
            data: this.pesg_list,
            // data: [
            //   {
            //     value: 911,
            //     name: "普通名词"
            //   },
            //   {
            //     value: 810,
            //     name: "普通动词"
            //   },
            //   {
            //     value: 227,
            //     name: "副词"
            //   },
            //   {
            //     value: 220,
            //     name: "数量词"
            //   },
            //   {
            //     value: 197,
            //     name: "形容词"
            //   },
            //   {
            //     value: 189,
            //     name: "人名"
            //   },
            //   {
            //     value: 114,
            //     name: "代词"
            //   },
            //   {
            //     value: 79,
            //     name: "连词"
            //   },
            //   {
            //     value: 77,
            //     name: "时间"
            //   },
            //   {
            //     value: 40,
            //     name: "地名"
            //   },
            //   {
            //     value: 35,
            //     name: "介词"
            //   },
            //   {
            //     value: 35,
            //     name: "其他名词"
            //   },
            //   {
            //     value: 33,
            //     name: "方位名词"
            //   },
            //   {
            //     value: 32,
            //     name: "动名词"
            //   },
            //   {
            //     value: 22,
            //     name: "量词"
            //   },
            //   {
            //     value: 22,
            //     name: "处所名词"
            //   },
            //   {
            //     value: 16,
            //     name: "形副词"
            //   },
            //   {
            //     value: 9,
            //     name: "助词"
            //   },
            //   {
            //     value: 5,
            //     name: "机构名"
            //   },
            //   {
            //     value: 5,
            //     name: "名形词"
            //   }
            // ],
            // [
            //   { value: 335, name: "名词" },
            //   { value: 310, name: "动词" },
            //   { value: 234, name: "形容词" },
            //   { value: 135, name: "副词" },
            //   { value: 1548, name: "代词" }
            // ],
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