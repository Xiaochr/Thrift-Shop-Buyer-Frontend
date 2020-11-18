<template>
  <div class="bookview">
    
    <el-page-header @back="backHome" title=" " content="Userpage"></el-page-header>
    <el-divider></el-divider>
    <el-row>
    <el-col :span="10">
      <div class="block">
        <img :src="user_item.avatar">
      </div>
    </el-col>
    <el-col :span="14">
      <el-row>User Name: {{user_item.username}}</el-row>
      <el-row>Real Name: {{user_item.real_name}}</el-row>
      <el-row>Age: {{user_item.age}}</el-row>
      <el-row>Gender: {{user_item.sex}}</el-row>
      <el-row>Telephone: {{user_item.telephone}}</el-row>
      <el-row>Certification Type: {{user_item.certificationType}}</el-row>
      <el-row>Certification Number: {{user_item.certificationNumber}}</el-row>
      <el-row>Address: {{user_item.address}}</el-row>
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
            <el-table-column prop="order_id" label="Order ID"></el-table-column>
            <el-table-column prop="order_time" label="Order Time"></el-table-column>
            <el-table-column prop="postageFee" label="Postage Fee"></el-table-column>
            <el-table-column label="Detail">
              <template slot-scope="scope">
                <el-button type="primary" size="mini" @click="orderDetail(scope.row)">Detail</el-button>
              </template>
            </el-table-column>
          </el-table>
        </el-tab-pane>
        <el-tab-pane label="Orders to be Delivered" name="deliver">Comments</el-tab-pane>
        <el-tab-pane label="Orders in Transportation" name="transport">Comments</el-tab-pane>
        <el-tab-pane label="Orders to be Commented" name="comment">Comments</el-tab-pane>
        <el-tab-pane label="Finished Orders" name="finish">Comments</el-tab-pane>
      </el-tabs>
    </el-card>

    

    <el-dialog title="Edit User Info" :visible="editVisible" @close="closeEdit">
      <el-form>
        <el-row>
          <el-col :span="8">
            <el-form-item label="User name">
              <el-input type="text" v-model="user_item.username" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="7"><el-form-item></el-form-item></el-col>
          <el-col :span="8">
            <el-form-item label="Password">
              <el-input type="text" v-model="user_item.password" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
        
        <el-row>
          <el-col :span="8">
            <el-form-item label="Real name">
              <el-input type="text" v-model="user_item.real_name" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="1"><el-form-item></el-form-item></el-col>
          <el-col :span="7">
            <el-form-item label="Age">
              <el-input type="text" v-model="user_item.age" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="1"><el-form-item></el-form-item></el-col>
          <el-col :span="7">
            <el-form-item label="Gender">
              <el-input type="text" v-model="user_item.sex" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
        
        <el-row>
          <el-col :span="8">
            <el-form-item label="Certification type">
              <el-input type="text" v-model="user_item.certificationType" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="7"><el-form-item></el-form-item></el-col>
          <el-col :span="8">
            <el-form-item label="Certification number">
              <el-input type="text" v-model="user_item.certificationNumber" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-col>
        </el-row>

        <el-row>
          <el-form-item label="Address">
            <el-input type="text" v-model="user_item.address" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
          </el-form-item>
        </el-row>

        <el-row>
          <el-col :span="8">
            <el-form-item label="Telephone">
              <el-input type="text" v-model="user_item.telephone" placeholder="" oninput="if(value.length>10) value=value.slice(0,10)"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="7"><el-form-item></el-form-item></el-col>
          <el-col :span="8">
            <el-form-item></el-form-item>
          </el-col>
        </el-row>

      </el-form>
      <span slot="footer">
        <el-button type="success" plain @click="editUserInfo()">Save</el-button>
        <el-button type="primary" plain @click="resetUserInfo()">Reset</el-button>
        <el-button type="primary" plain @click="closeEdit()">Cancel</el-button>
      </span>
    </el-dialog>

    <el-dialog title="Order Detail" :visible="detailVisible" @close="detailVisible = false">
      <el-table class="data-table" :data="user_order" stripe border style="height: 100%">
        <el-table-column prop="order_id" label="Order ID"></el-table-column>
        <el-table-column prop="entry_id" label="Book ID"></el-table-column>
        <el-table-column prop="order_id" label="Book Name"></el-table-column>
        <el-table-column prop="number" label="Number"></el-table-column>
        <el-table-column prop="seller_id" label="Seller ID"></el-table-column>
        <el-table-column prop="postageFee" label="Postage Fee"></el-table-column>
        <el-table-column prop="status" label="Status"></el-table-column>
      </el-table>
      <span slot="footer">
        <el-button type="success" plain @click="confirmArrival">Confirm Arrival</el-button>
        <el-button type="primary" plain @click="detailVisible = false">Close</el-button>
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
      order_detail: [],
      active_name: "all",
      editVisible: false,
      detailVisible: false,
      refreshFlag: 0 
    }
  },
  methods: {
    backHome() {
      location.assign('../homepage.html')
    },
    getItems() {
      var id_dict = {'user_id': 1}
      console.log(id_dict)
      this.$http.post('http://124.70.178.153:8085/user_info', id_dict).then(
        function(data) {
          console.log(data);
          this.user_item = data.body
        }
      )
      .catch(
        function(data) {
          console.log(data)
          this.$notify({
            title: 'Error',
            message: 'Fail to get data!',
            duration: 6000
          })
        }
      )
    },
    getOrders() {
      var id_dict = {'user_id': 1}
      console.log(id_dict)
      this.$http.post('http://124.70.178.153:8085/user_order_' + this.active_name, id_dict).then(
        function(data) {
          console.log(data);
          this.user_order = data.body
        }
      )
      .catch(
        function(data) {
          console.log(data)
          this.$notify({
            title: 'Error',
            message: 'Fail to get data!',
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
      this.$http.post('http://124.70.178.153:8085/edit_user_info', this.user_item).then(
        function(data) {
          console.log(data);
          this.refreshFlag ++
          this.editVisible = false
        }
      )
      .catch(
        function(data) {
          console.log(data)
          this.$notify({
            title: 'Error',
            message: 'Fail to save data!',
            duration: 6000
          })
        }
      )
    },
    orderDetail(row) {
      this.detailVisible = true
      this.$http.get('http://124.70.178.153:8085/user_order_detail/'+row.order_id.toString()).then(
        function(data) {
          console.log(data);
          this.order_detail = data.body
        }
      )
      .catch(
        function(data) {
          console.log(data)
          this.$notify({
            title: 'Error',
            message: 'Fail to get data!',
            duration: 6000
          })
        }
      )
    },
    confirmArrival() {
      this.detailVisible = false
      this.$http.post('http://124.70.178.153:8085/confirm_receive', this.order_detail).then(
        function(data) {
          console.log(data);
          this.order_detail = data.body
        }
      )
      .catch(
        function(data) {
          console.log(data)
          this.$notify({
            title: 'Error',
            message: 'Fail to confirm arrival!',
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
