<template>
  <div class="admin">
    <PageHeader></PageHeader>
    <el-container>
      <el-aside width="150px">
        <el-menu :default-active="tableType" :style="{'min-height': '500px'}">
          <el-menu-item index="user" @click="getTableData('user')"><i class="el-icon-s-custom"></i>用户管理</el-menu-item>
          <el-menu-item index="strategy" @click="getTableData('strategy')"><i class="el-icon-s-data"></i>策略管理</el-menu-item>
        </el-menu>
      </el-aside>
      <el-main>
        <el-table class="data-table" :data="tableData">
          <el-table-column :key="obj.label" v-for="obj in tableCols" :label="obj.label" :prop="obj.prop" :width="obj.width" :sortable="obj.prop!='operator'"></el-table-column>
        </el-table>
      </el-main>
    </el-container>
  </div>
</template>

<script>
import PageHeader from '../components/PageHeader'
import axios from 'axios'

export default {
  data () {
    return {
      tableType: 'user',
      tableData: [],
      tableCols: []
    }
  },
  components: {
    'PageHeader': PageHeader
  },
  created () {
    this.getTableData(this.tableType)
  },
  methods: {
    getTableData: function (type) {
      this.tableType = type
      if (type === 'user') {
        this.tableCols = [
          {label: '用户名', prop: 'name', width: 150},
          {label: '用户id', prop: 'id', width: 100},
          {label: '手机号', prop: 'phone', width: 150},
          {label: '会员等级', prop: 'level', width: 100},
          {label: '创建时间', prop: 'create_time'},
          {label: '登录时间', prop: 'last_login_time'},
          {label: '登录次数', prop: 'login_count'}
          // {label: '操作', prop: 'operator', width: 150}
        ]
        this.getUserlist()
      } else {
        this.tableCols = [
          {label: '策略名', prop: 'name', width: 150},
          {label: '策略id', prop: 'id', width: 150},
          {label: '策略描述', prop: 'desc', width: 250},
          {label: '策略权限', prop: 'visibility', width: 100},
          {label: '首页显示', prop: 'show_in_home', width: 100},
          {label: '创建时间', prop: 'create_time'},
          {label: '更新时间', prop: 'upd_time'}
          // {label: '操作', prop: 'operator', width: 150}
        ]
        this.getStrategyList()
      }
    },
    getUserlist: function () {
      axios.get('/user/list')
        .then(res => {
          let result = res.data || {}
          if (result.success) {
            this.tableData = result.data
          }
          console.log(result)
        }, error => {
          console.log(error)
        })
    },
    getStrategyList: function () {
      axios.get('/strategy/list')
        .then(res => {
          let result = res.data || {}
          if (result.success) {
            this.tableData = result.data
          }
          console.log(result)
        }, error => {
          console.log(error)
        })
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../assets/scss/pages/Admin.scss"
</style>
