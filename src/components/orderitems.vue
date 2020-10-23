<template>
  <div class="orderitems">
    <el-card class="table-card">
      <el-page-header @back="to_shopping_cart" title=" " content="Order Placement"></el-page-header>
      <el-divider></el-divider>
      <el-card>
        <el-row>
          <el-col :span="2">
            <span>Name: </span>
          </el-col>
          <el-col :span="6">
            <el-input v-model="info.name" disabled></el-input>
          </el-col>
          <el-col :span="2">
            <span>Tel: </span>
          </el-col>
          <el-col :span="6">
            <el-input v-model="info.tel" disabled></el-input>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="2">
            <span>Address: </span>
          </el-col>
          <el-col :span="14">
            <el-input v-model="info.address" disabled></el-input>
          </el-col>
          <el-col :span="8">
            <el-button type="primary" icon="el-icon-edit" @click="change_address">Change Address</el-button>
          </el-col>
        </el-row>
        
      </el-card>
      <el-divider></el-divider>
      <el-table class="data-table" :data="items" stripe border style="height: 100%">
        <el-table-column prop="name" label="Book name"></el-table-column>
        <el-table-column prop="price" label="Price"></el-table-column>
        <el-table-column prop="inventory" label="Inventory"></el-table-column>
        
      </el-table>
      
    </el-card>
    
    <el-dialog :visible="chVisible" @close="close_change">
      <el-form>
        <el-row>
          <el-col :span="8">
            <el-form-item label="Name">
              <el-input type="text" v-model="info.name" placeholder="Please input name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="2"><p> </p></el-col>
          <el-col :span="8">
            <el-form-item label="Tel.">
              <el-input type="text" v-model="info.tel" placeholder="Please input tel number"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="12">
           <el-form-item label="Address">
              <el-input type="text" v-model="info.address" placeholder="Please input address"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
      </el-form>
      <span slot="footer">
        <el-button type="success" plain @click="save_change">Confirm</el-button>
        <el-button type="primary" plain @click="close_change">Cancel</el-button>
      </span>
    </el-dialog>


  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [], //存储要在表格中显示的数据
      info: {
        "name": "TY Wong",
        "tel": 1234,
        "address": "Tsinghua"
      },
      origin_info: {},
      cur_item: {}, //当前的一条记录
      curIndex: 1, //当前的index
      curLen: 0, //当前数据数量
      chVisible: false,
      refreshFlag: 0 //是否刷新页面
    }
  },
  methods: {
    getItems() {// 向后台发送请求，获取所有原料信息
      this.$http.get('http://127.0.0.1:8000/backend/info/').then(
        function(data) {
          console.log(data);
          this.items = data.body
          this.curLen = this.items[this.items.length - 1].mID
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
    editMaterial(row, curIndex) {// 弹出编辑对话框
      this.cur_item = row
      //this.orig_item = Object.assign({}, this.cur_item),
      this.curIndex = curIndex
      this.$http.post('http://127.0.0.1:8000/backend/info/search/', this.cur_item, {emulateJSON: true}).then(
        function(data) {
          console.log(data)
        }
      )
      location.assign('../book_detail.html')
    },
    change_address() {
      this.chVisible = true
      this.origin_info = Object.assign({}, this.info)
    },
    save_change() {
      this.chVisible = false
    },
    close_change() {
      this.info = Object.assign({}, this.origin_info)
      this.chVisible = false
    },
    to_shopping_cart() {
      location.assign('../shopping_cart.html')
    }
  },
  watch: {
    refreshFlag() {
      this.getItems()
    },
  },
  mounted() {
    this.getItems()
  }
}
</script>

<style>
.table-card {
  width: 100%;
  height: 100%;
  margin-top: 50px auto;
  text-align: center;
}
.data-table {
  margin-top: 500px auto;
  height: 100%;
  text-align: center;
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
