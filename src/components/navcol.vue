<template lang="html">
  <div class="navcol">
    <el-menu :default-active="index" class="el-menu-vertical-demo" @open="handleOpen" @close="handleClose" 
    background-color="#696969" text-color="#fff" active-text-color="#ffd04b">
      <el-menu-item index="0" @click="backHome">
        <i class="el-icon-house"></i>
        <span slot="title">Homepage</span>
      </el-menu-item>
      <el-menu-item index="1" @click="to_shopping_cart">
        <i class="el-icon-shopping-cart-full"></i>
        <span slot="title">Shopping Cart</span>
      </el-menu-item>
      <el-menu-item index="2" @click="to_userpage">
        <i class="el-icon-user"></i>
        <span slot="title">Userpage</span>
      </el-menu-item>
      <el-menu-item index="3" @click.native="logoutVisible = true">
        <i class="el-icon-switch-button"></i>
        <span slot="title">Logout</span>
      </el-menu-item>
    </el-menu>

    <el-dialog title="Logout" :visible="logoutVisible" @close="logoutVisible = false">
      <span>Are you sure to log out?</span>
      <span slot="footer">
        <el-button type="danger" @click="confirmLogout()">Comfirm</el-button>
        <el-button type="primary" @click="logoutVisible = false">Cancel</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isCollapse: true,
      logoutVisible: false,
      
    }
  },
  methods: {
    backHome() {
      location.assign('../homepage.html')
    },
    to_shopping_cart() {
      //location.assign('../shopping_cart.html')
      this.$emit("cart_listen", true)
    },
    to_userpage() {
      location.assign('../userpage.html')
    },
    confirmLogout() {
      this.logoutVisible = false
      location.assign('../index.html')
    },
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    }
  }
}
</script>

<style lang="css">
.el-menu-vertical-demo {
  width: 100%;
  height: 100%;
}
</style>