<template>
  <div style="width: 100%; height: 100%; background-color: #fff;">
    <div style="height: 100%; width: 100%;">
      <div id="word_cloud" style="width:100%; height:100%;">
        <h2>{{'《'+this.name+'》' +'的评论特征提取词：'+ this.tfidf}}</h2>
      </div>
    </div>
  </div>
</template>

 <script>
import echarts from "echarts";
import axios from "axios";

export default {
  name: "word_cloud",
  props: ["jsonData_tfidf"],
  data() {
    return {
      tfidf: this.jsonData_tfidf.tfidf,
      name: this.jsonData_tfidf.name
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