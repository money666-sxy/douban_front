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
              <h1></h1>
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
              ></el-option>
            </el-select>
          </el-col>
          <el-col :span="6">
            <el-input
              placeholder="请输入内容"
              prefix-icon="el-icon-search"
              v-model="input2"
              style="width:350px;float:left"
            ></el-input>
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
                <el-menu-item key="chart_allscore" @click="selectTag('chart_allscore')">选项2</el-menu-item>
              </el-menu-item-group>
            </el-submenu>
            <el-submenu index="3">
              <template slot="title">
                <i class="el-icon-location"></i>主题分析
              </template>
              <el-menu-item-group>
                <el-menu-item key="chart_wordcloud" @click="selectTag('chart_wordcloud')">词云图</el-menu-item>
                <el-menu-item key="chart_wordpesg" @click="selectTag('chart_wordpesg')">词性图</el-menu-item>
              </el-menu-item-group>
            </el-submenu>
          </el-menu>
        </el-aside>
        <el-main>
          <div v-if="selected_tag=='chart_allscore'">
            <Allscore />
          </div>

          <div v-else-if="selected_tag=='chart_hist'">
            <Hist />
          </div>

          <div v-else-if="selected_tag=='chart_heatmap'">
            <Heatmap />
          </div>

          <div v-else-if="selected_tag=='chart_wordcloud'">
            <Wordcloud />
          </div>

          <div v-else-if="selected_tag=='chart_wordpesg'">
            <Wordpesg />
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

export default {
  name: "HelloWorld",
  components: {
    Allscore,
    Hist,
    Heatmap,
    Wordcloud,
    Wordpesg
  },
  data() {
    return {
      selected_tag: ""
    };
  },

  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    },
    selectTag(tag) {
      this.selected_tag = tag;
    }
  }
};
</script>
