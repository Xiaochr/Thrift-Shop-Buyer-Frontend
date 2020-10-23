<template lang="html">
  <div class="shoppingfooter">
    <el-row>
      <el-popover placement="top" width="400" trigger="hover">
        <cartitemsmini></cartitemsmini>
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
  data() {
    return {
      drawer: false,
    }
  },
  methods: {
    backHome() {
      location.assign('../homepage.html')
    },
    to_shopping_cart() {
      location.assign('../shopping_cart.html')
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