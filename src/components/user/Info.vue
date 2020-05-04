<template>
    <el-row class="demo-avatar demo-basic">
        <el-col>
            <div class="demo-basic--circle">
                <div class="block">
                    <el-avatar :size="80" :src="circleUrl">
                        <img src="user.avater" v-if="isLogin">
                        <img v-else src="https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png">
                    </el-avatar>
                    <p v-if="isLogin">username</p>
                    <p v-else>请登录</p>
                </div>
                <div class="auth" v-if="!isLogin">
                    <router-link to="/login">
                        <el-button type="primary">登录</el-button>
                    </router-link>

                    <router-link to="/register">
                        <el-button>注册</el-button>
                    </router-link>
                </div>
                <div class="info" v-else>
                    <el-button
                            type="primary"
                            @click="logout"
                            plain
                            v-loading.fullscreen.lock="fullscreenLoading"
                    >注销</el-button>
                </div>
            </div>
        </el-col>
    </el-row>
</template>

<script>
export default {
  name: 'UserInfo',
  data () {
    return {
      user: {},
      isLogin: false,
      fullscreenLoading: false
    }
  },
  methods: {
    checkLogin () {
      let token = this.$cookies.get('token')
      let user = this.$cookies.get('user')
      if (token.length === 0 || user.length === 0) {
        this.isLogin = false
      } else {
        this.isLogin = true
        this.user = user
      }
    },
    logout () {
      this.fullscreenLoading = true
      this.$http.post('http://laravel-blog-server.com/logout?user_id=' + this.user.id)
        .then(response => {
          this.fullscreenLoading = false
          this.isLogin = false
          this.$cookies.remove('user')
          this.$cookies.remove('token')
        })
        .catch(err => {
          this.$notify({
            title: '提示信息',
            message: err.message,
            type: 'error'
          })
          return false
        })
    }
  },
  mounted () {
    let that = this
    that.checkLogin()
  }
}
</script>

<style scoped>
.demo-basic--circle {
    margin-top: 20px;
}
</style>
