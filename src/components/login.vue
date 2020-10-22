<template lang="html">
  <div class="login">
    <el-card class="index-card">
      <div slot="header">
        Buyer Login
      </div>
      <el-form>
        <el-form-item label="User ID">
          <el-input v-model="id" placeholder="Please input user ID. "></el-input>
        </el-form-item>
        <el-form-item label="Password">
          <el-input v-model="pswd" placeholder="Please input the password. "></el-input>
        </el-form-item>
      </el-form>
      <el-button type="primary" plain @click="backHome">Login</el-button>
    </el-card>

  </div>
</template>

<script>
export default {
  data() {
    return {
      id: '',
      pswd: '',
      passFlag: false
    }
  },
  methods: {
    login() {// 登录
      this.$http.post('http://127.0.0.1:8000/backend/login/', {'id': this.id, 'pswd': this.pswd}, {emulateJSON: true}).then(
        function(data) {
          console.log(data)
          this.passFlag = data.body
        }
      )
      if (this.passFlag) {
        location.assign('../homepage.html')
      }
      else {
        this.$notify({
          title: 'Error',
          message: 'The wrong password!',
          duration: 6000
        })
      }
    },
    backHome() {// 为方便调试设置的假登录函数
      location.assign('../homepage.html')
    }
  }
}
</script>

<style lang="postcss">
.index-card {
  width: 400px;
  margin: 50px auto;
}
</style>
