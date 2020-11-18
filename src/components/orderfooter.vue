<template lang="html">
  <div class="orderfooter">
    <el-row>
      <el-col :span="10" style="text-align: right">
        <span style="font-size: 20px">
          Postage: ¥ {{postage}}, Total: ¥ {{total_price + postage}}
        </span>
      </el-col>
      <el-col :span="2"><p> </p></el-col>
      
      <el-col :span="4">
        <el-dropdown @command="handleCommand">
          <el-button type="primary">
            Payment<i class="el-icon-arrow-up el-icon--right"></i>
          </el-button>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item command="1">Alipay</el-dropdown-item>
            <el-dropdown-item command="0">WeChat Pay</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </el-col>
      <el-col :span="2"><p> </p></el-col>
      <el-col :span="6">
        <el-button type="danger" @click="cancelOrder">Cancel</el-button>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  props: ["cart_items", "total_price", "user_item", "postage", "order_id"],
  data() {
    return {
      drawer: false,
      success: true,
      message: "",
      command: 0
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
      console.log(this.cart_items)
      this.$http.post('http://124.70.178.153:8081/confirm_order', {"order_id": this.order_id, "customer_id": 1, "order_detail": this.cart_items, "action": 1, "PaymentType": command}).then(
        function(data) {
          console.log(data);
          this.success = data.success
          this.message = data.message
          this.$notify({
            title: 'Success',
            message: this.message,
            duration: 6000
          })
        }
      )
      .catch(
        function(data) {
          console.log(data)
          this.$notify({
            title: 'Failed',
            message: this.message,
            duration: 6000
          })
        }
      )
    },
    cancelOrder() {
      console.log(this.cart_items)
      this.$http.post('http://124.70.178.153:8081/confirm_order', {"order_id": this.order_id, "customer_id": 1, "order_detail": this.cart_items, "action": 0, "PaymentType": this.command}).then(
        function(data) {
          console.log(data);
          this.success = data.success
          this.message = data.message
          this.$notify({
            title: 'Success',
            message: this.message,
            duration: 6000
          })
        }
      )
      .catch(
        function(data) {
          console.log(data)
          this.$notify({
            title: 'Failed',
            message: this.message,
            duration: 6000
          })
        }
      )
      this.$emit("cancel_order_listen", false)
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