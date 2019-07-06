<template>
  <div class="page-header">
    <div class="wrapper">
      <div class="web-title">RichTech</div>
      <div class="user-cnt">
        <div class="user-info" v-if="data.isLogin">
          <img class="user-avatar" src="../assets/images/user_default_grey.png">
          <span class="user-name">data.uname</span>
        </div>
        <el-button type="text" @click="data.loginDialogVisible=true" v-else>登录</el-button>
        <LoginDialog :loginDialogVisible.sync="data.loginDialogVisible"></LoginDialog>
      </div>
    </div>
  </div>
</template>

<script>
import LoginDialog from './LoginDialog'
import axios from 'axios'

export default {
  data () {
    return {
      data: {
        loginDialogVisible: false
      }
    }
  },
  created () {
    this.getUserInfo()
  },
  components: {
    'LoginDialog': LoginDialog
  },
  methods: {
    getUserInfo: () => {
      axios.get('/user/info')
        .then(res => {
          let info = res.data || {}
          if (info.uid) {
            this.data.uname = info.name
            this.data.uid = info.uid
          }
        }, rejected => {
          console.log(rejected)
        })
    }
  },
  computed: {
    isLogin: () => {
      return this.data.uid
    }
  }
}
</script>

<style lang="scss">
@import "../assets/scss/components/PageHeader.scss"
</style>
