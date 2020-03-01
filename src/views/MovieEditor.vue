<template>
  <el-row v-loading="loading">
    <el-col :span="12" :offset="4">
      <el-form v-bind:model="movie" label-position="top">
        <el-row>
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
          <el-col :span="16">
            <el-form-item label="豆瓣地址">
              <el-input v-model="movie.doubanUrl"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
        <el-form-item label="上线">
          <el-button v-on:click="movie.launches.push({name:''})">增加</el-button>
          <el-button v-on:click="movie.launches.pop()">减少</el-button>
        </el-form-item>
        <el-row :gutter="20">
          <el-col :span="8" v-for="(launch, index) in movie.launches" v-bind:key="index">
            <el-form-item label="类型">
              <el-select v-model="launch.type">
                <el-option
                  v-for="(launch,index) in launches"
                  v-bind:key="index"
                  v-bind:label="launch.label"
                  v-bind:value="launch.value"
                ></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="日期">
              <el-date-picker v-model="launch.date" type="date"></el-date-picker>
            </el-form-item>
          </el-col>
        </el-row>
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
      loading: false,
      movie: {
        doubanUrl: "",
        id: 0,
        chineseName: "",
        countries: [],
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
          value: "剧集",
          label: "剧集"
        }
      ],
      launches: [
        {
          value: "蓝光",
          label: "蓝光"
        },
        {
          value: "美版",
          label: "美版"
        },
        {
          value: "韩版",
          label: "韩版"
        },
        {
          value: "Netflix",
          label: "Netflix"
        }
      ]
    };
  },
  methods: {
    submit: function() {
      this.loading = true;
      this.$axios
        .post("/movie/", this.movie)
        .then(
          function(response) {
            this.loading = false;
            this.$message("提交成功！");
            this.movie = response.data.object;
          }.bind(this)
        )
        .catch(
          function() {
            this.loading = false;
            this.$message("提交失败！");
          }.bind(this)
        );
    }
  }
};
</script>