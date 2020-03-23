<template>
    <el-row :gutter="24" type="flex" justify="space-around" align="middle">
        <el-col :span="6">
            <div class="grid-content bg-purple">
                <router-link to="/" class="web-title">
                    {{ webName }}
                </router-link>
            </div>
        </el-col>
        <el-col :span="6" >
            <app-searchbar class="app-searchbar"></app-searchbar>
        </el-col>
        <el-col :span="12">
                <app-menu-list :data="menuData" class="app-menu-list"></app-menu-list>
        </el-col>
    </el-row>
</template>

<script>
import HeaderMenuList from '../menu/HeaderMenuList'
import SearchBar from '../searchbar/SearchBar'
const url = 'http://laravel-blog-server.com'
export default {
  name: 'app-header',
  components: {
    'app-menu-list': HeaderMenuList,
    'app-searchbar': SearchBar
  },
  data: function () {
    return {
      webName: '我的博客',
      activeIndex: '/',
      menuData: {}
    }
  },
  mounted () {
    let that = this
    that.loadMenu()
  },
  methods: {
    loadMenu () {
      this.$http.get(url + '/load_menu')
        .then(response => {
          if (response.data.code === 200) {
            this.menuData = response.data.data
          }
        }).catch(err => {
          console.log(err)
        })
    }
  },
  created () {
    // console.log(this.$route.path);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .el-row {
        margin-bottom: 20px;
    }
    .el-col {
        border-radius: 4px;
    }
    .bg-purple {
        background: #ff2;
    }
    .web-title{
        font-size: 2em;
    }
    .router-link-active {
        text-decoration: none;
    }
    .app-menu-list{
        float: right;
    }
    .el-col-6,.el-col-12{
        width: 100%;
        height: 61px;
        line-height: 55px;
        background-color: #fff;
    }
</style>
