<template>
  <el-dialog title="用户登录" :visible.sync="isVisible">
  <el-form :model="form">
    <el-form-item label="用户名" :label-width="formLabelWidth">
      <el-input v-model="form.name" autocomplete="off"></el-input>
    </el-form-item>
    <el-form-item label="密码" :label-width="formLabelWidth">
      <el-input v-model="form.password" type="password" autocomplete="off"></el-input>
    </el-form-item>
  </el-form>
  <div slot="footer" class="dialog-footer">
    <el-button @click="closeDialog()">取 消</el-button>
    <el-button type="primary" @click="loginUser()">确 定</el-button>
  </div>
  </el-dialog>
</template>

<script>
export default {
  props: {
    loginDialogVisible: Boolean
  },
  data () {
    return {
      formLabelWidth: '60px',
      form: {
        name: '',
        password: ''
      }
    }
  },
  created () {
    this.form.name = ''
    this.form.password = ''
  },
  methods: {
    closeDialog: function () {
      this.isVisible = false
    },
    loginUser: function () {

    }
  },
  computed: {
    isVisible: {
      get: function () {
        return this.loginDialogVisible
      },
      set: function (newVal) {
        // console.log('this', this)
        // console.log('this', this.formLabelWidth)
        this.$emit('update:loginDialogVisible', newVal)
      }
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
