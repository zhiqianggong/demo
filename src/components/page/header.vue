<template>
  <div>
    <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal">
      <el-menu-item index="1">Dashboard</el-menu-item>
      <el-menu-item index="2">Services</el-menu-item>
      <el-menu-item index="3">History</el-menu-item>
      <el-menu-item index="4">Actions</el-menu-item>
      <el-input size="medium" class="reset-input" placeholder="Search..">
      <i slot="prefix" class="el-input__icon el-icon-search"></i>
    </el-input>
    </el-menu>
  </div>
</template>

<script>
export default {
    data() {
        return {
            activeIndex: '1',
        }
    }
};
</script>

<style>
.reset-input {
    position: absolute;
    max-width: 200px;
    line-height: 60px;
    float: right;
}
.reset-input .el-input__inner {

    border-radius: 15px;
}
</style>