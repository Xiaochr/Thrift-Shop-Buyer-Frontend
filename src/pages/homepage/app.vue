<template>
  <div id="app">
    <el-container style="height: 100%" direction="vertical">
      <el-header>Header</el-header>
      <el-container>
        <el-aside width="200px">
          <navcol style="height: 100%"></navcol>
        </el-aside>
        <el-container>
          <el-main>This is homepage</el-main>
          <el-footer>Footer</el-footer>
        </el-container>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import navcol from '../../components/navcol.vue'
export default {
  components: {
    navcol
  },
  data() {
    return {
      msg: 'Use Vue 2.0 Today!'
    }
  }
}
</script>

<style lang="postcss">
.table-card {
  width: 1000px;
  margin-top: 50px auto;
  text-align: center;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 20px;
}
body {
  background: #F5F5F5;
}
html,
body,
#app,
.app,
.el-container {
  padding: 0px;
  margin: 0px;
  height: 100%;
}
.el-header, .el-footer {
  background-color: #B3C0D1;
  color: #333;
  text-align: center;
}
</style>
