<template lang="html">
  <div class="orderfooter">
    <el-row>
      <el-col :span="18" style="text-align: right">
        Total: ¥ 100
      </el-col>
      <el-col :span="2"><p> </p></el-col>
      <el-col :span="4">
        <el-dropdown @command="handleCommand">
          <el-button type="primary">
            Payment<i class="el-icon-arrow-up el-icon--right"></i>
          </el-button>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item command="a">Alipay</el-dropdown-item>
            <el-dropdown-item command="w">WeChat Pay</el-dropdown-item>
            <el-dropdown-item command="d">Debit Card</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </el-col>
    </el-row>

    

  </div>
</template>

<script>
export default {
  data() {
    return {
      drawer: false,
    }
  },
  methods: {
    backHome() {
      location.assign('../homepage.html')
    },
    to_orderpage() {
      location.assign('../orderpage.html')
    },
    handleCommand(command) {
      this.$notify({
        title: 'Success',
        message: 'Successful payment',
        duration: 6000
      })
      this.backHome()
    }
  }
}
</script>

<style lang="css">
.orderfooter {
  line-height: 100%;
  font-size: 40px;
}

</style>