<template lang="html">
  <div class="siteheader">
    <el-row>
      <el-col :span="16" style="text-align: left">
        <el-button type="info" icon="el-icon-reading" @click="backHome" circle></el-button>
        Thrift Book Store
      </el-col>
      <el-col :span="2"><p> </p></el-col>
      <el-col :span="6" style="text-align: right">
        Welcome, Wong
        <el-button type="info" icon="el-icon-user" @click="to_userpage" circle></el-button>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  data() {

  },
  methods: {
    backHome() {
      location.assign('../homepage.html')
    },
    to_userpage() {
      location.assign('../userpage.html')
    }
  }
}
</script>

<style lang="css">
.siteheader {
  line-height: 100%;
  font-size: 24px;
}

</style>