<template>
  <div class="cartitemsmini">
    <el-card class="table-card">
      
      <el-table class="data-table" :data="items" stripe border style="height: 100%">
        <el-table-column prop="name" label="Book name"></el-table-column>
        <el-table-column prop="price" label="Price"></el-table-column>
        <el-table-column prop="inventory" label="Unit"></el-table-column>
        
      </el-table>
      <el-divider></el-divider>
      <el-row>
        <el-col :span="16">
          ¥ 100
        </el-col>
        <el-col :span="4"><p> </p></el-col>
        <el-col :span="4">
          <el-button type="primary" @click="to_shopping_cart">Order</el-button>
        </el-col>
      </el-row>
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
    editMaterial(row, curIndex) {// 弹出编辑对话框
      this.cur_item = row
      //this.orig_item = Object.assign({}, this.cur_item),
      this.curIndex = curIndex
      this.$http.post('http://127.0.0.1:8000/backend/info/search/', this.cur_item, {emulateJSON: true}).then(
        function(data) {
          console.log(data)
        }
      )
      location.assign('../book_detail.html')
    },
    to_shopping_cart() {
      location.assign('../shopping_cart.html')
    }
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
}
.data-table {
  margin-top: 500px auto;
  height: 100%;
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
