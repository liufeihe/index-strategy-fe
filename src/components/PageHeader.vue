<template>
  <div class="page-header">
    <div class="wrapper">
      <div class="web-title" @click="goHome()">RichTech</div>
      <LoginDialog></LoginDialog>
    </div>
  </div>
</template>

<script>
import LoginDialog from './LoginDialog'

export default {
  data () {
    return {}
  },
  components: {
    'LoginDialog': LoginDialog
  },
  methods: {
    goHome: function () {
      this.$router.push('/')
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../assets/scss/components/PageHeader.scss"
</style>
