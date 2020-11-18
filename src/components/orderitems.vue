<template>
  <div class="orderitems">
    <el-card class="table-card">
      <el-card>
        <el-row>
          <el-col :span="2">
            <span>Name: </span>
          </el-col>
          <el-col :span="6">
            <el-input v-model="user_item.username" disabled></el-input>
          </el-col>
          <el-col :span="2">
            <span>Tel: </span>
          </el-col>
          <el-col :span="6">
            <el-input v-model="user_item.telephone" disabled></el-input>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="2">
            <span>Address: </span>
          </el-col>
          <el-col :span="14">
            <el-input v-model="user_item.address" disabled></el-input>
          </el-col>
          <el-col :span="8">
            <el-button type="primary" icon="el-icon-edit" @click="change_address">Change Address</el-button>
          </el-col>
        </el-row>
      </el-card>
      <el-divider></el-divider>

      <el-table class="data-table" :data="cart_items" stripe border style="height: 100%">
        <el-table-column prop="name" label="Book name"></el-table-column>
        <el-table-column prop="price" label="Price"></el-table-column>
        <el-table-column prop="inventory" label="Unit"></el-table-column>
      </el-table>
    </el-card>

    <orderfooter :cart_items="cart_items" :total_price="total_price" :user_item="user_item" :postage="postage" :order_id="order_id" @cancel_order_listen="cancel_order"></orderfooter>
    
    <el-dialog :visible="chVisible" @close="close_change">
      <el-form>
        <el-row>
          <el-col :span="8">
            <el-form-item label="Name">
              <el-input type="text" v-model="user_item.username" placeholder="Please input name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="2"><p> </p></el-col>
          <el-col :span="8">
            <el-form-item label="Tel.">
              <el-input type="text" v-model="user_item.telephone" placeholder="Please input tel number"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="12">
           <el-form-item label="Address">
              <el-input type="text" v-model="user_item.address" placeholder="Please input address"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
      </el-form>
      <span slot="footer">
        <el-button type="success" plain @click="save_change">Confirm</el-button>
        <el-button type="primary" plain @click="close_change">Cancel</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
import orderfooter from './orderfooter.vue'
export default {
  components: {
    orderfooter
  },
  props: ["cart_items", "total_price", "user_item", "order_id", "postage"],
  data() {
    return {
      items: [], 
      origin_info: {},
      chVisible: false,
      refreshFlag: 0 
    }
  },
  methods: {
    change_address() {
      this.chVisible = true
      this.origin_info = Object.assign({}, this.info)
    },
    save_change() {
      this.chVisible = false
      // save changed address
    },
    close_change() {
      this.info = Object.assign({}, this.origin_info)
      this.chVisible = false
    },
    to_shopping_cart() {
      location.assign('../shopping_cart.html')
    },
    cancel_order() {
      this.$emit("cancel_order_listen", false)
    }
  },
  watch: {
    refreshFlag() {
      
    },
  },
  mounted() {
    
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
