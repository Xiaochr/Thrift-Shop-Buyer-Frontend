<template lang="html">
  <div class="cartfooter">
    <el-row>
      <el-col :span="18" style="text-align: right">
        Total: ¥ 100
      </el-col>
      <el-col :span="2"><p> </p></el-col>
      <el-col :span="4">
        <el-button type="primary" @click="to_orderpage">Order</el-button>
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