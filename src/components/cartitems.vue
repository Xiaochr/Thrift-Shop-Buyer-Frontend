<template>
  <div class="cartitems">
    <el-card class="table-card">
      <el-page-header @back="backHome" title=" " content="Shopping Cart"></el-page-header>
      <el-divider></el-divider>
      <el-table class="data-table" :data="items" stripe border style="height: 100%">
        <el-table-column prop="name" label="Book name"></el-table-column>
        <el-table-column prop="price" label="Price"></el-table-column>
        <el-table-column prop="inventory" label="Unit"></el-table-column>
        
      </el-table>
      
    </el-card>
    

  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [], //存储要在表格中显示的数据
      cur_item: {}, //当前的一条记录
      curIndex: 1, //当前的index
      curLen: 0, //当前数据数量
      searchContent: '', //存储需要搜索的内容
      refreshFlag: 0 //是否刷新页面
    }
  },
  methods: {
    backHome() {// 返回主页
      location.assign('../homepage.html')
    },
    getItems() {// 向后台发送请求，获取所有原料信息
      this.$http.get('http://127.0.0.1:8000/backend/info/').then(
        function(data) {
          console.log(data);
          this.items = data.body
          this.curLen = this.items[this.items.length - 1].mID
        }
      )
      .catch(
        function(data) {
          console.log(data)
          this.$notify({
            title: '错误',
            message: '获取数据失败！',
            duration: 6000
          })
        }
      )
    },
    del_item() {
      this.items
    },
  },
  watch: {
    refreshFlag() {
      this.getItems()
    },
  },
  mounted() {
    this.getItems()
  }
}
</script>

<style>
.table-card {
  width: 100%;
  height: 100%;
  margin-top: 50px auto;
  text-align: center;
}
.data-table {
  margin-top: 500px auto;
  height: 100%;
  text-align: center;
}
.el-row {
  margin-bottom: 20px;
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
</style>
