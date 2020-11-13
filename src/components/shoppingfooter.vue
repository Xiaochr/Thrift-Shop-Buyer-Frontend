<template lang="html">
  <div class="shoppingfooter">
    <el-row>
      <el-popover placement="top" width="400" trigger="hover">
        <cartitemsmini :cart_items="cart_items" :total_price="total_price"></cartitemsmini>

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
      total_price: 0
    }
  },
  methods: {
    backHome() {
      location.assign('../homepage.html')
    },
    to_shopping_cart() {
      //location.assign('../shopping_cart.html')
      this.$emit("cart_listen", true)
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