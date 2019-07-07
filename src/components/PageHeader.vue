<template>
  <div class="page-header">
    <div class="wrapper">
      <div class="web-title">RichTech</div>
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
  }
}
</script>

<style lang="scss" scoped>
@import "../assets/scss/components/PageHeader.scss"
</style>
