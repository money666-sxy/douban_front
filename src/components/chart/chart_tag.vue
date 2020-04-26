<template>
  <div style="width: 100%; height: 100%; background-color: #fff;">
    <div style="height: 100%; width: 100%;">
      <div id="tag" style="width:100%; height:620px;">
        <h2>{{this.name +'的主题标签：'+ this.tag}}</h2>
      </div>
    </div>
  </div>
</template>

 <script>
import echarts from "echarts";
import axios from "axios";

export default {
  name: "tag",
  props: ["jsonData_tag"],
  data() {
    return {
      tag: this.jsonData_tag.tag,
      name: this.jsonData_tag.name
    };
  },
  mounted() {
    // this.getSource();
  },
  methods: {
    // getSource() {
    //   axios.get("http://127.0.0.1:8000/wordcloud/").then(response => {
    //     this.wordcloud = response.data.wordcloud_image;
    //     this.name = response.data.name;
    //     // console.log(typeof this.bookinfo);
    //     // console.log(response.data.wordcloud_image);
    //   });
    // }
  }
};
</script>