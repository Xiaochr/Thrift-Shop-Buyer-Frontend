<template>
  <div class="cartitems">
    <el-card class="table-card">
      <el-table class="data-table" :data="cart_items" stripe border style="height: 100%">
        <el-table-column prop="name" label="Book name"></el-table-column>
        <el-table-column prop="author" label="Author"></el-table-column>
        <el-table-column prop="price" label="Price"></el-table-column>
        <el-table-column prop="inventory" label="Unit"></el-table-column>
        <el-table-column label="Edit">
          <template slot-scope="scope">
            <el-button type="danger" size="mini" icon="el-icon-delete" @click="delItem(scope.row, scope.$index)">Delete</el-button>
          </template>
        </el-table-column>
      </el-table>
      <el-divider></el-divider>

      <el-row>
        <el-col :span="18" style="text-align: right">
          Total: {{total_price}}
        </el-col>
        <el-col :span="2"><p> </p></el-col>
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
    backHome() {
      location.assign('../homepage.html')
    },
    delItem(row, curIndex) {
      this.cart_items.splice(curIndex, 1)
      this.$emit("price_listen")
    },
    to_orderpage() {
      this.$emit("order_listen", true)
    }
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
