<template>
  <el-row>
    <el-col :span="12" :offset="4">
      <el-form v-bind:model="movie" label-position="top">
        <el-row :gutter="20">
          <el-col :span="12">
            <el-form-item label="中文名称">
              <el-input v-model="movie.chineseName"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="源名称">
              <el-input v-model="movie.originName"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row :gutter="20">
          <el-col :span="12">
            <el-form-item label="导演">
              <el-button v-on:click="movie.directors.push({})">增加</el-button>
              <el-button v-on:click="movie.directors.pop()">减少</el-button>
            </el-form-item>
            <el-form-item v-for="(director, index) in movie.directors" v-bind:key="index">
              <el-input v-model="director.name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="主演">
              <el-button v-on:click="movie.starrings.push({})">增加</el-button>
              <el-button v-on:click="movie.starrings.pop()">减少</el-button>
            </el-form-item>
            <el-form-item v-for="(starring, index) in movie.starrings" v-bind:key="index">
              <el-input v-model="starring.name"></el-input>
            </el-form-item>
          </el-col>
        </el-row>

        <el-form-item label="标签">
          <el-checkbox-group v-model="movie.tags">
            <el-checkbox v-bind:label="tag" v-for="(tag, index) in tags" v-bind:key="index"></el-checkbox>
          </el-checkbox-group>
        </el-form-item>
        <el-row :gutter="20">
          <el-col :span="8">
            <el-form-item label="上映日期">
              <el-date-picker v-model="movie.releaseDate" type="date"></el-date-picker>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="评分">
              <el-input-number
                v-model="movie.score"
                :step="0.1"
                :min="0"
                :max="10"
                :precision="1"
                :controls="false"
              ></el-input-number>
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="类型">
              <el-select v-model="movie.type">
                <el-option
                  v-for="(type,index) in types"
                  v-bind:key="index"
                  v-bind:label="type.label"
                  v-bind:value="type.value"
                ></el-option>
              </el-select>
            </el-form-item>
          </el-col>
        </el-row>
        <el-form-item label="简介">
          <el-input type="textarea" v-bind:autosize="{minRows: 4}" v-model="movie.introduction"></el-input>
        </el-form-item>

        <el-form-item label="上线">
          <el-button v-on:click="movie.launches.push({})">增加</el-button>
          <el-button v-on:click="movie.launches.pop()">减少</el-button>
        </el-form-item>
        <el-row :gutter="20">
          <el-col :span="8" v-for="(launch, index) in movie.launches" v-bind:key="index">
            <el-form-item label="类型">
              <el-input v-model="launch.type"></el-input>
            </el-form-item>
            <el-form-item label="日期">
              <el-date-picker v-model="launch.date" type="date"></el-date-picker>
            </el-form-item>
          </el-col>
        </el-row>

        <el-form-item label="海报链接">
          <el-input v-model="movie.posterUrl"></el-input>
        </el-form-item>
        <el-form-item label="海报预览">
          <el-image v-bind:src="movie.posterUrl">
            <div slot="error">
              <i class="el-icon-picture-outline"></i>
            </div>
          </el-image>
        </el-form-item>

        <el-form-item>
          <el-button v-on:click="submit()">提交</el-button>
        </el-form-item>
      </el-form>
    </el-col>
  </el-row>
</template>
<script>
export default {
  name: "Movie",
  data: function() {
    return {
      active: 1,
      movie: {
        id: 1,
        chineseName: "",
        directors: [],
        introduction: "",
        launches: [],
        originName: "",
        posterUrl: "",
        releaseDate: "",
        score: 0.0,
        starrings: [],
        tags: [],
        type: ""
      },
      types: [
        {
          value: "电影",
          label: "电影"
        },
        {
          value: "电视剧",
          label: "电视剧"
        }
      ],
      tags: [
        "剧情",
        "喜剧",
        "动作",
        "爱情",
        "科幻",
        "动画",
        "悬疑",
        "惊悚",
        "恐怖",
        "犯罪",
        "同性",
        "音乐",
        "歌舞",
        "传记",
        "历史",
        "战争",
        "西部",
        "奇幻",
        "冒险",
        "灾难",
        "武侠",
        "情色"
      ]
    };
  },
  methods: {
    submit: function() {
      this.$axios
        .post(
          "/movie/",
          this.movie,
          function() {
            this.$message("提交成功！");
          }.bind(this)
        )
        .catch(
          function() {
            this.$message("提交失败！");
          }.bind(this)
        );
    }
  }
};
</script>