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
            <shoppingfooter @cart_listen="open_shopping_cart"></shoppingfooter>
          </el-footer>
        </el-container>
      </el-container>
    </el-container>

    <el-dialog title="Book Detail" :visible="toDetail" @close="toDetail = false">
      <bookinfo @add_listen="add_to_cart" :entry_id="entry_id" style="height: 100%; width: 100%"></bookinfo>
    </el-dialog>

    <el-dialog title="Shopping Cart" :visible="toCart" @close="toCart = false">
      <cartitems style="height: 100%; width: 100%"></cartitems>
      <cartfooter @order_listen="open_orderpage" @change_listen="update_cart"></cartfooter>
    </el-dialog>

    <el-dialog title="Order Placement" :visible="toOrder" @close="toOrder = false">
      <orderitems style="height: 100%; width: 100%"></orderitems>
      <orderfooter></orderfooter>
    </el-dialog>
  </div>
</template>

<script>
import navcol from '../../components/navcol.vue'
import bookview from '../../components/bookview.vue'
import siteheader from '../../components/siteheader.vue'
import shoppingfooter from '../../components/shoppingfooter.vue'
import cartitems from '../../components/cartitems.vue'
import cartfooter from '../../components/cartfooter.vue'
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
    cartfooter,
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
      cart_items: []
    }
  },
  methods: {
    open_shopping_cart(message) {
      this.toCart = message
    },
    open_orderpage(message) {
      this.toOrder = message
      this.toCart = false
    },
    open_book_detail(message, entry_id) {
      this.toDetail = message
      this.entry_id = entry_id
    },
    add_to_cart(message) {
      this.cart_items.push(message)
    },
    update_cart(message) {
      this.cart_items = Object.assign([], message)
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
