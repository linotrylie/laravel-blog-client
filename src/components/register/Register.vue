<template>
    <div class="main">
        <div class="register-container">
            <h3>注册</h3>
            <div class="form-container">
                <el-form :model="form" :rules="rules" ref="form"  label-width="70px" class="demo-ruleForm">
                    <el-form-item label="用户名" prop="name">
                        <el-input v-model="form.name" placeholder="用户名" type="text" style="width:80%"/>
                    </el-form-item>
                    <el-form-item label="邮箱" prop="email" label-width="70px">
                        <el-input v-model="form.email" placeholder="邮箱" type="text" style="width:80%"/>
                    </el-form-item>
                    <el-form-item label="密码" prop="password" label-width="70px">
                        <el-input v-model="form.password" placeholder="密码" type="password" style="width:80%"/>
                    </el-form-item>
                    <el-form-item label="确认密码" prop="confirm_password" label-width="70px">
                        <el-input v-model="form.confirm_password" placeholder="确认密码" type="password" style="width:80%"/>
                    </el-form-item>
                    <el-form-item>
                        <el-button type="primary" @click="submitForm('form')">提交</el-button>
                        <el-button @click="resetForm('form')">重置</el-button>
                    </el-form-item>
                </el-form>
            </div>
        </div>

    </div>
</template>

<script>
export default {
  name: 'register',
  data () {
    let checkName = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入用户名'))
      } else {
        callback()
      }
    }
    let checkPassword = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入密码'))
      } else {
        callback()
      }
    }
    let checkEmail = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入邮箱'))
      } else {
        callback()
      }
    }
    let checkConfirmPassword = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入确认密码'))
      } else {
        callback()
      }
    }
    return {
      form: {
        name: '',
        password: '',
        email: '',
        confirm_password: ''
      },
      rules: {
        name: [
          {validator: checkName, trigger: 'blur'}
        ],
        password: [
          {validator: checkPassword, trigger: 'blur'}
        ],
        email: [
          {validator: checkEmail, trigger: 'blur'}
        ],
        confirm_password: [
          {validator: checkConfirmPassword, trigger: 'blur'}
        ]
      }
    }
  },
  mounted () {
    let that = this
    that.isLogin()
  },
  methods: {
    resetForm (formName) {
      this.$refs[formName].resetFields()
    },
    submitForm (formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          this.$http.post('laravel-blog-server.com/register', this.form)
            .then(res => {
              if (res.data.code === 200) {
                this.$notify({
                  title: '提示信息',
                  message: res.data.message,
                  type: 'success'
                })

                this.$router.push({path: '/login'})
              } else {
                this.$notify({
                  title: '提示信息',
                  message: res.data.message,
                  type: 'error'
                })
              }
              console.log(res)
            })
            .catch(err => {
              console.log(err)
            })
        } else {
          this.$notify({
            title: '提示信息',
            message: '输入信息不符合规则，请认真填写！',
            type: 'error'
          })
          return false
        }
      })
    },
    isLogin () {
      if (this.$cookies.get('user_id')) {
        this.$router.push({path: '/'})
      }
    }
  }
}
</script>

<style scoped>

    body{
        width: 100%;
        height: 100%;
        margin: 0 auto;
        padding: 0;
    }
    .main {
        margin: 0 auto;
        padding: 0;
        width: 100%;
        height: 100%;
        display: flex;
        background-image: linear-gradient(to bottom right,#66b1ff,#fef0f0);
        z-index:1;
    }
    .register-container{
        width: 450px;
        height: 420px;
        border: 1px solid #6cb2eb;
        mso-border-shadow: yes;
        border-radius: 15px;
        margin: 110px auto;
        justify-content: center;
        background-image: linear-gradient(to bottom right,rgb(	100,149,237),rgb(176,196,222)) ;
        z-index: 10;
    }
    h3{
        text-align: center;
        margin-top: 10px;
    }
    .form-container {
        /*margin-right: 20px;*/
        margin-top: 20px;
        text-align: center;

    }

</style>
