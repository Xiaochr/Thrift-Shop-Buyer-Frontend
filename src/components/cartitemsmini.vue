<template>
  <div class="cartitemsmini">
    <el-card class="table-card">
      <el-table class="data-table" :data="cart_items" stripe border style="height: 100%">
        <el-table-column prop="name" label="Book name"></el-table-column>
        <el-table-column prop="author" label="Author"></el-table-column>
        <el-table-column prop="price" label="Price"></el-table-column>
        <el-table-column prop="inventory" label="Unit"></el-table-column>
      </el-table>
      <el-divider></el-divider>

      <el-row>
        <el-col :span="16">
          Total: {{total_price}}
        </el-col>
        <el-col :span="4"><p> </p></el-col>
        <el-col :span="4">
          <el-button type="primary" @click="to_orderpage">Order</el-button>
        </el-col>
      </el-row>
    </el-card>
  </div>
</template>

<script>
export default {
  props: ["cart_items", "total_price"],
  data() {
    return {
      
    }
  },
  methods: {
    to_orderpage() {
      this.$emit("order_listen", true)
    }
  },
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
