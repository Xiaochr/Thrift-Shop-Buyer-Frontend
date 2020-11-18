<template lang="html">
  <div class="shoppingfooter">
    <el-row>
      <el-popover placement="top" width="400" trigger="hover">
        <cartitemsmini :cart_items="cart_items" :total_price="total_price" @order_listen="to_orderpage"></cartitemsmini>
        <el-button slot="reference" type="primary" icon="el-icon-shopping-cart-full" plain @click="to_shopping_cart">Shopping Cart</el-button>
      </el-popover>
    </el-row>
  </div>
</template>

<script>
import cartitemsmini from './cartitemsmini.vue'
export default {
  components: {
    cartitemsmini
  },
  props: ["cart_items", "total_price"],
  data() {
    return {
      
    }
  },
  methods: {
    backHome() {
      location.assign('../homepage.html')
    },
    to_shopping_cart() {
      this.$emit("cart_listen", true)
    },
    to_orderpage() {
      this.$emit("order_listen", true)
    }
  }
}
</script>

<style lang="css">
.shoppingfooter {
  line-height: 100%;
  font-size: 40px;
}

</style>