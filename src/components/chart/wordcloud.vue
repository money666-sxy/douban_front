<template>
  <div style="width: 100%; height: 100%; background-color: #fff;">
    <div style="height: 100%; width: 100%;">
      <div id="word_cloud" style="width:100%; height:620px;">
        <el-image :src="this.wordcloud" alt="评论词云"></el-image>
        <!-- <img
          src="/Users/money666/Desktop/django_douban/douban_front/src/static/chart_wordcloud.png"
          alt="评论词云"
        />-->
        <!-- <h1>{{this.wordcloud}}</h1> -->
      </div>
    </div>
  </div>
</template>

 <script>
import echarts from "echarts";
import axios from "axios";

export default {
  name: "word_cloud",
  props: ["jsonData_wordcloud"],
  data() {
    return {
      wordcloud: this.jsonData_wordcloud.word_cloud,
      name: this.jsonData_wordcloud.name
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