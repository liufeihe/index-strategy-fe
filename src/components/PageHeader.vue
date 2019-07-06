<template>
  <div class="page-header">
    <div class="wrapper">
      <div class="web-title">RichTech</div>
      <div class="user-cnt">
        <div class="user-info" v-if="isLogin">
          <img class="user-avatar" src="../assets/images/user_default_grey.png">
          <span class="user-name">Anonymous</span>
        </div>
        <el-link v-else>登录</el-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      isLogin: true
    }
  }
}
</script>

<style lang="scss">
@import "../assets/scss/components/PageHeader.scss"
</style>
