<template>
  <div id="app">
    <el-container style="height: 800px; border: 1px solid #eee">
      <el-header>
        <el-row>
          <el-col :span="6">
            <a href="http://120.55.41.64/">
              <img
                src="../assets/logo_youtubew.png"
                alt="money666友情链接"
                style="height: 60px;float:left;"
              />
            </a>
          </el-col>
          <el-col :span="6">
            <div>
              <h2 v-if="isShowTip">没有搜索到结果</h2>
            </div>
          </el-col>
          <el-col :span="6">
            <el-select v-model="value" placeholder="请选择类别" style="width:120px;float:right">
              <el-option
                v-for="item in options"
                :key="item.value"
                :label="item.label"
                :value="item.value"
                :disabled="item.disabled"
                style="height:100%"
              ></el-option>
            </el-select>
          </el-col>
          <el-col :span="6">
            <el-input
              placeholder="请输入内容"
              prefix-icon="el-icon-search"
              v-model="input_search"
              style="width:250px;float:left"
            ></el-input>
            <!-- <el-autocomplete
              class="inline-input"
              v-model="state1"
              :fetch-suggestions="querySearch"
              placeholder="请输入内容"
              @select="handleSelect"
              style="width:250px;float:left;height:100%"
            ></el-autocomplete>-->
            <el-button type="primary" icon="el-icon-search" @click="search">搜索</el-button>
          </el-col>
        </el-row>
      </el-header>
      <el-container>
        <el-aside width="200px" style="background-color: rgb(238, 241, 246)">
          <el-menu
            default-active="2"
            class="el-menu-vertical-demo"
            @open="handleOpen"
            @close="handleClose"
          >
            <el-submenu index="1">
              <template slot="title">
                <i class="el-icon-location"></i>基本信息
              </template>
              <el-menu-item-group>
                <el-menu-item
                  class="menu-item"
                  key="chart_allscore"
                  @click="selectTag('chart_allscore')"
                >总评分</el-menu-item>
                <el-menu-item
                  class="menu-item"
                  key="chart_hist"
                  @click="selectTag('chart_hist')"
                >直方图</el-menu-item>
              </el-menu-item-group>
            </el-submenu>
            <el-submenu index="2">
              <template slot="title">
                <i class="el-icon-location"></i>评论热度
              </template>
              <el-menu-item-group>
                <el-menu-item key="chart_heatmap" @click="selectTag('chart_heatmap')">热力图</el-menu-item>
                <!-- <el-menu-item key="test" @click="selectTag('test')">选项2</el-menu-item> -->
              </el-menu-item-group>
            </el-submenu>
            <el-submenu index="3">
              <template slot="title">
                <i class="el-icon-location"></i>评论主题分析
              </template>
              <el-menu-item-group>
                <el-menu-item key="chart_tag" @click="selectTag('chart_tag')">主题标签</el-menu-item>
                <el-menu-item key="chart_tfidf" @click="selectTag('chart_tfidf')">评论特征提取</el-menu-item>
                <el-menu-item key="chart_wordcloud" @click="selectTag('chart_wordcloud')">评论词云</el-menu-item>
                <el-menu-item key="chart_wordpesg" @click="selectTag('chart_wordpesg')">评论词性</el-menu-item>
              </el-menu-item-group>
            </el-submenu>
          </el-menu>
        </el-aside>
        <el-main>
          <div v-if="selected_tag=='chart_allscore'">
            <Allscore :jsonData_score="datalist"></Allscore>
          </div>

          <div v-else-if="selected_tag=='chart_hist'">
            <Hist :jsonData_star="datalist"></Hist>
          </div>

          <div v-else-if="selected_tag=='chart_heatmap'">
            <!-- <Heatmap /> -->
            <Heatmap :jsonData_heat="datalist"></Heatmap>
          </div>

          <div v-else-if="selected_tag=='test'">
            <Test :jsonData="datalist"></Test>
          </div>

          <div v-else-if="selected_tag=='chart_tag'">
            <Tag :jsonData_tag="datalist"></Tag>
          </div>

          <div v-else-if="selected_tag=='chart_wordcloud'">
            <Wordcloud :jsonData_wordcloud="datalist"></Wordcloud>
          </div>

          <div v-else-if="selected_tag=='chart_tfidf'">
            <Tfidf :jsonData_tfidf="datalist"></Tfidf>
          </div>

          <div v-else-if="selected_tag=='chart_wordpesg'">
            <Wordpesg :jsonData_pesg="datalist"></Wordpesg>
          </div>
        </el-main>
      </el-container>
      <el-footer></el-footer>
    </el-container>
  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.el-header {
  background-color: #b3c0d1;
  color: #333;
  text-align: center;
  line-height: 60px;
}

.el-footer {
  background-color: #b3c0d1;
  color: #333;
  text-align: center;
  line-height: 120px;
}

.el-aside {
  background-color: #d3dce6;
  color: #333;
  text-align: center;
  line-height: 200px;
}

.el-main {
  background-color: #e9eef3;
  color: #333;
  text-align: center;
  line-height: 160px;
}

body > .el-container {
  margin-bottom: 40px;
}

.el-container:nth-child(5) .el-aside,
.el-container:nth-child(6) .el-aside {
  line-height: 260px;
}

.el-container:nth-child(7) .el-aside {
  line-height: 320px;
}
</style>


<script>
import Allscore from "./chart/all_score.vue";
import Hist from "./chart/star_hist.vue";
import Wordpesg from "./chart/wordpesg_rose.vue";
import Wordcloud from "./chart/wordcloud.vue";
import Heatmap from "./chart/heatmap.vue";
import Test from "./chart/test.vue";
import Tag from "./chart/chart_tag.vue";
import Tfidf from "./chart/chart_tfidf.vue";
import axios from "axios";

export default {
  name: "HelloWorld",
  components: {
    Allscore,
    Hist,
    Heatmap,
    Wordcloud,
    Wordpesg,
    Test,
    Tag,
    Tfidf
  },
  data() {
    return {
      selected_tag: "",
      options: [
        {
          value: "选项1",
          label: "读书"
        },
        {
          value: "选项2",
          label: "电影",
          disabled: true
        },
        {
          value: "选项3",
          label: "音乐",
          disabled: true
        }
      ], //下拉选择框列表
      input_search: "", //搜索框内容
      isShowTip: false, //搜索显示数据，当搜索不到数据时为true
      value: ""
      // restaurants: [],
      // state1: ""
    };
  },

  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    },
    search() {
      var word = this.input_search;
      console.log(word);
      axios({
        url: "http://127.0.0.1:8000/search",
        params: { bookname: word },
        method: "get"
      }).then(res => {
        console.log(res.data);
        this.datalist = res.data;
      });
    },

    // querySearch(queryString, cb) {
    //   var restaurants = this.restaurants;
    //   var results = queryString
    //     ? restaurants.filter(this.createFilter(queryString))
    //     : restaurants;
    //   // 调用 callback 返回建议列表的数据
    //   cb(results);
    // },
    // createFilter(queryString) {
    //   return restaurant => {
    //     return (
    //       restaurant.value.toLowerCase().indexOf(queryString.toLowerCase()) ===
    //       0
    //     );
    //   };
    // },
    // loadAll() {
    //   return [
    //     { value: "图书1" },
    //     { value: "图书2" },
    //     { value: "图书3" },
    //     { value: "图书4" },
    //     { value: "图书5" },
    //     { value: "图书6" },
    //     { value: "图书7" }
    //   ];
    // },
    handleSelect(item) {
      console.log(item);
    },
    selectTag(tag) {
      this.selected_tag = tag;
    }
  },
  mounted() {
    this.search();
    // this.restaurants = this.loadAll();
  }
};
</script>
