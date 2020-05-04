<template>
  <div id="app" :style="backgroundImage" style="background-size: 100%">
    <el-container>
      <el-header>
          <app-header/>
      </el-header>
      <el-main>
        <router-view/>
      </el-main>
      <el-footer>
          <app-footer/>
      </el-footer>
    </el-container>
  </div>
</template>

<script>
import AppFooter from './components/home/Footer'
import AppHeader from './components/home/Header'
import allBackgroundImages from './images/bg'
export default {
  name: 'App',
  components: {AppHeader, AppFooter},
  data () {
    return {
      isFixed: false, // bar浮动
      offsetTop: 0, // 触发bar浮动的阈值
      marginTop: 0, // 触发bar浮动的同时 给数据列表一个margin-top 防止列表突然上移 会很突兀
        allBackgroundImages
    }
  },
  mounted () {
    // 设置初始的 padding-bottom 值为 footer 的高度 +20 防止数据列表拉到最下面被footer挡住 +多少自定
    // this.paddingBottom = document.querySelector('.footer').offsetHeight + 20 + 'px'

    // 设置bar浮动阈值为 #fixedBar 至页面顶部的距离
    this.offsetTop = document.querySelector('#fixedBar').offsetTop

    // 开启滚动监听
    window.addEventListener('scroll', this.handleScroll)
  },
  methods: {
    // 滚动监听 滚动触发的效果写在这里
    handleScroll () {
      var scrollTop = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop

      if (scrollTop >= this.offsetTop) {
        this.isFixed = true
        this.marginTop = document.querySelector('#fixedBar').offsetHeight + 'px'
      } else {
        this.isFixed = false
        this.marginTop = 0
      }
    }
  },
  destroyed () {
    window.removeEventListener('scroll', this.handleScroll) // 离开页面 关闭监听 不然会报错
  },
    computed:{
        backgroundImage() {
            // 根据背景图数组的长度随机选择索引
            const randIndex = Math.floor(Math.random() * this.allBackgroundImages.length)
            return {
                // 获取对应的图片资源并将其设置到`background-image`属性上
                backgroundImage: `url(${this.allBackgroundImages[randIndex]})`
            }
        }
    }
}
</script>

<style>
    #app {
        /*font-family: 'Avenir', Helvetica, Arial, sans-serif;*/
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        /*color: #2c3e50;*/
        /*background-image: url("./assets/img/app/app-background-image.jpg");*/
    }
    img {
        width: 100%;
        height: 100%;
    }
::-webkit-scrollbar {
  width: 0 !important;
}
::-webkit-scrollbar {
  width: 0 !important;height: 0;
}
    .el-header{
        box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
        top: 0;
        width: 100%;
    }
    .el-main{
        width: 100%;
        margin-top: 60px;
    }
</style>
