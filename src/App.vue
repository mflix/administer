<template>
  <el-container id="app">
    <el-aside>
      <el-row>
        <el-col>
          <el-menu default-active="1" router>
            <el-menu-item index="/">首页</el-menu-item>
            <el-submenu index="/">
              <template slot="title">
                <span>电影</span>
              </template>
              <el-menu-item-group>
                <el-menu-item index="/movie/">列表</el-menu-item>
                <el-menu-item index="/movie/editor/">编辑</el-menu-item>
              </el-menu-item-group>
            </el-submenu>
            <el-menu-item index="/login/">登录</el-menu-item>
            <el-menu-item index="/logout/">注销</el-menu-item>
          </el-menu>
        </el-col>
      </el-row>
    </el-aside>
    <el-container>
      <el-main>
        <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  name: "app",
  data: function() {
    return {};
  }
};
</script>
