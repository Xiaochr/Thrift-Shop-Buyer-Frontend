<template>
  <div class="bookview">
    <el-card class="table-card">
      <el-row>
      <el-col :span="10">
        <div class="block">
          <img :src="'data:image/png;base64,' + book_info.image">
        </div>
      </el-col>
      <el-col :span="14">
        <el-row>Book Name: {{book_info.name}}</el-row>
        <el-row>Author: {{book_info.author}}</el-row>
        <el-row>Category: {{book_info.category}}</el-row>
        <el-row>Price: {{book_info.price}}</el-row>
        <el-row>Original Price: {{book_info.original_price}}</el-row>
        <el-row>
          <el-button type="primary" icon="el-icon-shopping-cart" @click="add_book">Add to Cart</el-button>
        </el-row>
      </el-col>
      </el-row>
      
      <el-card>
        <el-tabs v-model="active_name" @tab-click="handleClick">
          <el-tab-pane label="Book Detail" name="detail">{{book_info.description}}</el-tab-pane>
          <el-tab-pane label="User Comments" name="comment">{{book_info.entry_comment}}</el-tab-pane>
        </el-tabs>
      </el-card>
    </el-card>
  </div>
</template>

<script>
export default {
  props: ["book_info"],
  data() {
    return {
      active_name: "detail",
      refreshFlag: 0 
    }
  },
  methods: {
    backHome() {
      location.assign('../homepage.html')
    },
    add_book() {
      this.book_info.inventory = 1
      this.$emit("add_listen", this.book_info)
    },
    handleClick(tab, event) {
      console.log(tab, event);
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
