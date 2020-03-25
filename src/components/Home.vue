<template>
  <div class="home">
    <el-row :gutter="20" flex="flex" justify="center" align="middle">
      <el-col :span="14" :offset="3">
        <div class="post-list">
            <List></List>
        </div>
      </el-col>
      <el-col :span="4" :offset="1">
        <div class="aside">
          <div class="my">
            <UserInfo></UserInfo>
          </div>
          <div class="messagebox"></div>
          <div class="link"></div>
        </div>
      </el-col>
    </el-row>
    <el-tooltip placement="top" content="返回顶部">
      <!-- 组件使用 -->
      <BackToTop
              transitionName="fade"
              :visibilityHeight="300"
              :backPosition="0">
      </BackToTop>
    </el-tooltip>
  </div>
</template>

<script>
import BackToTop from '@/components/backtop/Backtop'
import List from '@/components/post/List'
import UserInfo from '@/components/user/Info'
export default {
  name: 'Home',
  components: { List, BackToTop, UserInfo },
  data () {
    return {
    }
  },
  methods: {

  },
  mounted () {

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  ::-webkit-scrollbar {
    width: 0 !important;
  }
  ::-webkit-scrollbar {
    width: 0 !important;height: 0;
  }
  .el-col-17{
    height: 600px;
    z-index: 1;
  }
  .my{
    height: 300px;
    width: 300px;
    box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
  }
  .messagebox{
      height: 300px;
      width: 300px;
      background-color: burlywood;
      margin-top: 20px;
  }
  .link {
      height: 300px;
      width: 300px;
      background-color: burlywood;
      margin-top: 20px;
  }
  .aside{
    height: 100px;
  }
</style>
