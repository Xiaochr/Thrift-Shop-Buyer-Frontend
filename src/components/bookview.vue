<template>
  <div class="bookview">
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
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [], 
      cur_item: {}, 
      searchContent: '', 
      refreshFlag: 0 
    }
  },
  methods: {
    backHome() {
      location.assign('../homepage.html')
    },
    getItems() {
      this.$http.get('http://124.70.178.153:8081/book').then(
        function(data) {
          console.log(data);
          this.items = data.body.book_info
        }
      )
      .catch(
        function(data) {
          console.log(data)
          this.$notify({
            title: 'Error',
            message: 'Failed to get data',
            duration: 6000
          })
        }
      )
    },
    bookDetail(row, curIndex) {
      this.cur_item = row
      this.$emit("detail_listen", true, row.entry_id)
    },
    searchName() {
      this.$http.post('http://124.70.178.153:8081/search_book', {'book_name': this.searchContent}, {emulateJSON: true}).then(
        function(data) {
          console.log(data)
          this.items = data.body
        }
      )
      .catch(
        function(data) {
          console.log(data)
          this.$notify({
            title: 'Error',
            message: 'Failed to search',
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
