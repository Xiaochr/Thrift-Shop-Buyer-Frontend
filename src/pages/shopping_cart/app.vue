<template>
  <div id="app">
    <el-container style="height: 100%; width: 100%" direction="vertical">
      <el-header>
        <siteheader></siteheader>
      </el-header>
      <el-container>
        <el-aside width="16%">
          <navcol style="height: 100%"></navcol>
        </el-aside>
        <el-container style="height: 100%; width: 100%">
          <el-main>
            <cartitems style="height: 100%; width: 100%"></cartitems>
          </el-main>
          <el-footer>
            
          </el-footer>
        </el-container>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import navcol from '../../components/navcol.vue'
import bookview from '../../components/bookview.vue'
import siteheader from '../../components/siteheader.vue'
import cartitems from '../../components/cartitems.vue'
export default {
  components: {
    navcol,
    bookview,
    siteheader,
    cartitems
  },
  data() {
    return {
      msg: 'Use Vue 2.0 Today!'
    }
  }
}
</script>

<style lang="postcss">
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
  width: 100%;
  height: 100%;
}
.el-header {
  background-color: #DCDCDC;
  color: #333;
  text-align: center;
}
.el-footer {
  background-color: #F5F5F5;
  color: #333;
  text-align: center;
}
.siteheader {
  margin-top: 0.8%;
}
</style>
