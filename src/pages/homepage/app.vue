<template>
  <div id="app">
    <el-container style="height: 100%; width: 100%" direction="vertical">
      <el-header>
        <siteheader></siteheader>
      </el-header>
      <el-container>
        <el-aside width="16%">
          <navcol style="height: 100%" @cart_listen="open_shopping_cart"></navcol>
        </el-aside>
        <el-container style="height: 100%; width: 100%">
          <el-main>
            <bookview @detail_listen="open_book_detail" style="height: 100%; width: 100%"></bookview>
          </el-main>
          <el-footer>
            <shoppingfooter :cart_items="cart_items" :total_price="total_price" @cart_listen="open_shopping_cart" @order_listen="open_orderpage"></shoppingfooter>
          </el-footer>
        </el-container>
      </el-container>
    </el-container>

    <el-dialog title="Book Detail" :visible="toDetail" @close="toDetail = false">
      <bookinfo @add_listen="add_to_cart" :entry_id="entry_id" style="height: 100%; width: 100%"></bookinfo>
    </el-dialog>

    <el-dialog title="Shopping Cart" :visible="toCart" @close="toCart = false">
      <cartitems :cart_items="cart_items" :total_price="total_price" @order_listen="open_orderpage" @price_listen="calculate_total_price" @change_listen="update_cart" style="height: 100%; width: 100%"></cartitems>
    </el-dialog>

    <el-dialog title="Order Placement" :visible="toOrder" @close="toOrder = false">
      <orderitems :cart_items="cart_items" :total_price="total_price" :user_item="user_item" :order_id="order_id" :postage="postage" @cancel_order_listen="cancel_order" style="height: 100%; width: 100%"></orderitems>
      
    </el-dialog>
  </div>
</template>

<script>
import navcol from '../../components/navcol.vue'
import bookview from '../../components/bookview.vue'
import siteheader from '../../components/siteheader.vue'
import shoppingfooter from '../../components/shoppingfooter.vue'
import cartitems from '../../components/cartitems.vue'
import orderfooter from '../../components/orderfooter.vue'
import orderitems from '../../components/orderitems.vue'
import bookinfo from '../../components/bookinfo.vue'
export default {
  components: {
    navcol,
    bookview,
    siteheader,
    shoppingfooter,
    cartitems,
    orderitems,
    orderfooter,
    bookinfo
  },
  data() {
    return {
      toCart: false,
      toOrder: false,
      toDetail: false,
      entry_id: 0,
      total_price: 0,
      cart_items: [],
      user_item: {},
      order_id: 0,
      postage: 0
    }
  },
  methods: {
    calculate_total_price() {
      this.total_price = 0
      for(var i in this.cart_items){
        this.total_price += (parseFloat(this.cart_items[i].price) * parseFloat(this.cart_items[i].inventory))
      }
    },
    getUserInfo() {
      this.$http.post('http://124.70.178.153:8081/user_info', {'user_id': 1}, {emulateJSON: true}).then(
        function(data) {
          console.log(data);
          this.user_item = data.body
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
    open_shopping_cart(message) {
      this.toCart = message
      this.calculate_total_price()
    },
    open_orderpage(message) {
      if(this.cart_items.length){
        this.toOrder = message
        this.$http.post('http://124.70.178.153:8081/order_book', {"customer_id": 1, "order_detail": this.cart_items}).then(
          function(data) {
            console.log(data);
            this.success = data.success
            this.order_id = data.order_id
            this.postage = data.postage
            
            this.$notify({
              title: 'Success',
              message: "Successfully placed the order",
              duration: 6000
            })
          }
        )
        .catch(
          function(data) {
            console.log(data)
            this.$notify({
              title: 'Failed',
              message: "Fail to order",
              duration: 6000
            })
          }
        )
        this.toCart = false
      }
      else {
        this.$notify({
          title: 'Warning',
          message: "Empty shopping cart",
          duration: 6000
        })
      }
      
    },
    open_book_detail(message, entry_id) {
      this.toDetail = message
      this.entry_id = entry_id
    },
    add_to_cart(message) {
      this.toDetail = false
      this.cart_items.push(message)
      this.calculate_total_price()
    },
    update_cart(message) {
      this.cart_items = Object.assign([], message)
    },
    cancel_order(message) {
      this.toOrder = false
    }
  },
  watch: {
    refreshFlag() {
      this.calculate_total_price()
      this.getUserInfo()
    },
  },
  mounted() {
    this.calculate_total_price()
    this.getUserInfo()
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
  height: 100%;
  width: 100%;
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
