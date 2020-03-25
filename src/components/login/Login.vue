<template>
    <div class="main">
        <div class="login-container">
            <h3>登录</h3>
            <div class="form-container">
                <el-form :model="form" :rules="rules" ref="form" class="demo-ruleForm">
                    <el-form-item label="用户名" label-width="60px" prop="phone">
                        <el-input v-model="form.phone" placeholder="用户名" type="text" style="width: 80%"/>
                    </el-form-item>
                    <el-form-item label="密码" label-width="60px" prop="password">
                        <el-input v-model="form.password" placeholder="密码" type="password" style="width: 80%"/>
                    </el-form-item>
                    <el-checkbox v-model="form.remember">记住我？</el-checkbox>
                    <el-form-item style="margin-top: 10px">
                        <el-button type="primary" @click="submitForm('form')">提交</el-button>
                        <el-button @click="resetForm('form')">重置</el-button>
                    </el-form-item>
                </el-form>
            </div>
        </div>
    </div>
</template>

<script>
const url = 'http://laravel-blog-server.com'
export default {
  name: 'login',
  data () {
    let checkUserName = (rule, value, callback) => {
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
    return {
      form: {
        phone: '',
        password: '',
        remember: false
      },
      rules: {
        phone: [
          {validator: checkUserName, trigger: 'blur'}
        ],
        password: [
          {validator: checkPassword, trigger: 'blur'}
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
      this.form.remember = false
    },
    submitForm: function (formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          this.$http.post(url + '/login', this.form)
            .then(res => {
              if (res.data.code === 200) {
                this.$cookies.set('token', res.data.data.token)
                this.$cookies.set('user', res.data.data)
                this.$notify({
                  title: '提示信息',
                  message: res.data.message,
                  type: 'success'
                })
                this.$router.push({path: '/'})
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
    .login-container{
        width: 450px;
        height: 300px;
        border: 1px solid #6cb2eb;
        mso-border-shadow: yes;
        border-radius: 15px;
        margin: 200px auto;
        justify-content: center;
        background-image: linear-gradient(to bottom right,rgb(100,149,237),rgb(176,196,222)) ;
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
