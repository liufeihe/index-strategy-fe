<template>
  <div class="user-cnt">
        <div class="user-info" v-if="uid">
          <el-dropdown @command="handleCommand">
            <img class="user-avatar" src="../assets/images/user_default_grey.png">
            <span class="user-name">{{uname}}</span>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item command="admin" v-if="level>=10">管理页面</el-dropdown-item>
              <el-dropdown-item command="logout">登出</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </div>
        <el-button type="text" @click="isVisible=true" v-else>登录</el-button>
        <el-dialog title="用户登录" width="30%" :visible.sync="isVisible" @close="closeDialog()">
          <el-form :model="form">
            <el-form-item label="手机号" :label-width="formLabelWidth">
              <el-input v-model="form.name" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="密码" :label-width="formLabelWidth">
              <el-input v-model="form.password" type="password" autocomplete="off"></el-input>
            </el-form-item>
          </el-form>
          <div slot="footer" class="dialog-footer">
            <span class="red warning" v-show="form.warning">{{form.warning}}</span>
            <el-button @click="closeDialog()">取 消</el-button>
            <el-button type="primary" @click="loginUser()">确 定</el-button>
          </div>
        </el-dialog>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  props: {
    loginDialogVisible: Boolean
  },
  data () {
    return {
      isVisible: false,
      uid: '',
      uname: '',
      level: -1,
      formLabelWidth: '60px',
      form: {
        name: '',
        password: '',
        warning: ''
      }
    }
  },
  created () {
    this.getUserInfo()
    this.form.name = ''
    this.form.password = ''
  },
  methods: {
    getUserInfo: function () {
      axios.get('/user/info')
        .then(res => {
          let result = res.data || {}
          if (result.success) {
            let info = result.data || {}
            if (info.id) {
              this.uname = info.name
              this.uid = info.id
              this.level = info.level
            }
          }
        }, rejected => {
          console.log(rejected)
        })
    },
    handleCommand: function (command) {
      switch (command) {
        case 'logout' :
          axios.post('/user/logout', {uid: this.uid})
            .then(res => {
              let result = res.data || {}
              if (result.success) {
                this.uid = ''
              }
            }, err => {
              console.log(err)
            })
          break
        case 'admin':
          break
      }
    },
    closeDialog: function () {
      this.isVisible = false
      this.form.warning = ''
    },
    loginUser: function () {
      this.form.warning = ''
      if (!this.form.name || !this.form.password) {
        this.form.warning = '用户名或者密码不能为空。'
        return
      }
      axios.post('/user/signin', {phone: this.form.name, password: this.form.password})
        .then(res => {
          let result = res.data || {}
          if (result.success) {
            let info = result.data || {}
            if (info.id) {
              this.uname = info.name
              this.uid = info.id
              this.level = info.level
            }
            this.form.warning = ''
            this.closeDialog()
          } else {
            this.form.warning = result.message
          }
        }, error => {
          this.form.warning = error
        })
    }
  }
  // computed: {
  //   isVisible: {
  //     get: function () {
  //       return this.loginDialogVisible
  //     },
  //     set: function (newVal) {
  //       // console.log('this', this)
  //       // console.log('this', this.formLabelWidth)
  //       this.$emit('update:loginDialogVisible', newVal)
  //     }
  //   }
  // }
}
</script>

<style lang="scss" scoped>
  .user-info{
    display: flex;
    align-items: center;
    padding: 10px 0;
  }
  .user-avatar{
    height: 34px;
  }
  .user-name{
    display: inline-block;
    max-width: 100px;
    overflow: hidden;
    text-overflow: ellipsis;
    line-height: 34px;
  }
  span.warning{
    color: red;
  }
</style>
