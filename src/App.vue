<template>
  <div id="app">
    <el-row>
      <el-col :xs="18" :sm="18" :md="18" :lg="18" :xl="18" class="left-content">
        <Header></Header>
        <Home></Home>
      </el-col>
      <el-col :xs="4" :sm="4" :md="4" :lg="4" :xl="4" class="right-content">
        <HelloWorld msg="Welcome to Your Vue.js App" />
      </el-col>
    </el-row>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Header from "./components/page/header";
import Home from "./components/home/index";

export default {
  name: "app",
  components: {
    HelloWorld,
    Header,
    Home
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.left-content {
    padding: 0 50px;
}
</style>
