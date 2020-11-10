<template>
  <div class="bookview">
    <el-card class="table-card">
      <el-page-header @back="backHome" title=" " content="Book Overview"></el-page-header>
      <el-divider></el-divider>
      <el-row>
        <el-col :span="16">
          <el-input v-model="searchContent" @keyup.enter.native="searchName()" placeholder="Search book name"></el-input>
        </el-col>
        <el-col :span="1"><p> </p></el-col>
        <el-col :span="3">
          <el-button type="primary" icon="el-icon-search" plain @click="searchName()">Search</el-button>
        </el-col>
        <el-col :span="4"><p> </p></el-col>
      </el-row>
      <el-table class="data-table" :data="items" stripe border style="height: 100%">
        <el-table-column prop="name" label="Book name"></el-table-column>
        <el-table-column prop="author" label="Author"></el-table-column>
        <el-table-column prop="category" label="Category"></el-table-column>
        <el-table-column prop="original_price" label="Original price"></el-table-column>
        <el-table-column prop="price" label="Price"></el-table-column>
        <el-table-column prop="inventory" label="Inventory"></el-table-column>
        <el-table-column label="Book detail">
          <template slot-scope="scope">
            <el-button type="primary" size="mini" icon="el-icon-edit" @click="bookDetail(scope.row, scope.$index)">Detail</el-button>
          </template>
        </el-table-column>
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
      this.$http.get('http://124.70.178.153:8083/book').then(
        function(data) {
          console.log(data);
          this.items = data.body.book_info
          //this.curLen = this.items[this.items.length - 1].mID
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
    bookDetail(row, curIndex) {
      this.cur_item = row
      //this.orig_item = Object.assign({}, this.cur_item),
      //this.curIndex = curIndex

      this.$emit("detail_listen", true, row.entry_id)
    },
    searchName() {// 模糊搜索
      this.$http.post('http://124.70.178.153/backend/info/search/', {'mName': this.searchContent}, {emulateJSON: true}).then(
        function(data) {
          console.log(data)
          this.items = data.body
        }
      )
      .catch(
        function(data) {
          console.log(data)
          this.$notify({
            title: '错误',
            message: '搜索失败！',
            duration: 6000
          })
        }
      )
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
