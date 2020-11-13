<template>
  <div class="bookview">
    <el-card class="table-card">
      <el-page-header @back="backHome" title=" " content="Userpage"></el-page-header>
      <el-divider></el-divider>
      <el-row>
      <el-col :span="10">
        <div class="block">
          <img src="../assets/logo.png">
        </div>
      </el-col>
      <el-col :span="14">
        <el-row>User Name</el-row>
        <el-row>Real Name</el-row>
        <el-row>Age</el-row>
        <el-row>Gender</el-row>
        <el-row>Certification Type</el-row>
        <el-row>Address</el-row>
        <el-row>
          <el-button type="primary" icon="el-icon-edit" @click="openEdit">Edit Personal Info</el-button>
        </el-row>
      </el-col>
      </el-row>
      
      <el-card>
        <span>Orders</span>
        <el-divider></el-divider>
        <el-tabs v-model="active_name" @tab-click="handleClick">
          <el-tab-pane label="All Orders" name="all">
            <el-table class="data-table" :data="user_order" stripe border style="height: 100%">
              <el-table-column prop="name" label="Order ID"></el-table-column>
              <el-table-column prop="name" label="Book name"></el-table-column>
              <el-table-column prop="inventory" label="Inventory"></el-table-column>
              <el-table-column prop="price" label="Price"></el-table-column>
              <el-table-column prop="price" label="Order State"></el-table-column>
            </el-table>
          </el-tab-pane>
          <el-tab-pane label="Orders to be Delivered" name="deliver">Comments</el-tab-pane>
          <el-tab-pane label="Orders in Transportation" name="transport">Comments</el-tab-pane>
          <el-tab-pane label="Orders to be Commented" name="comment">Comments</el-tab-pane>
          <el-tab-pane label="Finished Orders" name="finish">Comments</el-tab-pane>
        </el-tabs>
      </el-card>

    </el-card>

    <el-dialog title="Edit User Info" :visible="editVisible" @close="closeEdit">
      <el-form>
      <el-row>
        <el-col :span="10">
          <div class="block">
            <img src="../assets/logo.png">
          </div>
        </el-col>
        <el-col :span="14">
          <el-row>
            <el-form-item label="User name">
              <el-input type="text" v-model="user_item.user_name" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-row>
          <el-row>
            <el-form-item label="Password">
              <el-input type="text" v-model="user_item.password" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-row>
          <el-row>
            <el-form-item label="Real name">
              <el-input type="text" v-model="user_item.real_name" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-row>
          <el-row>
            <el-form-item label="Age">
              <el-input type="text" v-model="user_item.age" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-row>
          <el-row>
            <el-form-item label="Gender">
              <el-input type="text" v-model="user_item.sex" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-row>
          <el-row>
            <el-form-item label="Certification type">
              <el-input type="text" v-model="user_item.certificationType" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-row>
          <el-row>
            <el-form-item label="Certification number">
              <el-input type="text" v-model="user_item.certificationNumber" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-row>
          <el-row>
            <el-form-item label="Address">
              <el-input type="text" v-model="user_item.address" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-row>
          <el-row>
            <el-form-item label="Telephone">
              <el-input type="text" v-model="user_item.telephone" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-row>
          <el-row>
            <el-form-item label="Account">
              <el-input type="text" v-model="user_item.account" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-row>

        </el-col>
      </el-row>
      </el-form>
      <span slot="footer">
        <el-button type="success" @click="editUserInfo()">Save</el-button>
        <el-button type="primary" @click="resetUserInfo()">Reset</el-button>
        <el-button type="primary" @click="closeEdit()">Cancel</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user_item: {}, 
      user_order: [],
      orig_item: {},
      active_name: "all",
      editVisible: false,
      curIndex: 1, //当前的index
      curLen: 0, //当前数据数量
      searchContent: '', //存储需要搜索的内容
      refreshFlag: 0 //是否刷新页面
    }
  },
  methods: {
    backHome() {// 返回主页
      location.assign('../homepage.html')
    },
    getItems() {// 向后台发送请求，获取所有原料信息
      this.$http.post('http://124.70.178.153:8083/user_info', {'user_id': 1}, {emulateJSON: true}).then(
        function(data) {
          console.log(data);
          this.user_item = data.body
          //this.curLen = this.items[this.items.length - 1].mID
        }
      )
      .catch(
        function(data) {
          console.log(data)
          this.$notify({
            title: '错误',
            message: '获取数据失败！',
            duration: 6000
          })
        }
      )
    },
    getOrders() {
      this.$http.post('http://124.70.178.153:8083/user_order_' + this.active_name, {'user_id': 1}, {emulateJSON: true}).then(
        function(data) {
          console.log(data);
          this.user_order = data.body
          //this.curLen = this.items[this.items.length - 1].mID
        }
      )
      .catch(
        function(data) {
          console.log(data)
          this.$notify({
            title: '错误',
            message: '获取数据失败！',
            duration: 6000
          })
        }
      )
    },
    openEdit() {
      this.editVisible = true
      this.orig_item = Object.assign({}, this.user_item)
    },
    closeEdit() {
      this.editVisible = false
      this.user_item = Object.assign({}, this.orig_item)
    },
    resetUserInfo() {
      this.user_item = Object.assign({}, this.orig_item)
    },
    editUserInfo() {
      this.$http.post('http://124.70.178.153:8083/edit_user_info', this.user_item, {emulateJSON: true}).then(
        function(data) {
          console.log(data);
          this.user_order = data.body
          this.refreshFlag ++
          this.editVisible = false
          //this.curLen = this.items[this.items.length - 1].mID
        }
      )
      .catch(
        function(data) {
          console.log(data)
          this.$notify({
            title: '错误',
            message: '获取数据失败！',
            duration: 6000
          })
        }
      )
    },
    handleClick(tab, event) {
      console.log(tab, event);
    }
  },
  watch: {
    refreshFlag() {
      this.getItems()
    },
  },
  mounted() {
    this.getItems()
    this.getOrders()
  }
}
</script>

<style>
.table-card {
  width: 100%;
  height: 100%;
  margin-top: 50px auto;
}
.data-table {
  margin-top: 500px auto;
  height: 100%;
}
.el-row {
  margin-bottom: 20px;
}
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
</style>
