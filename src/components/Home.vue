<template>
  <div class="home">
    <el-row :gutter="20" flex="flex" justify="center" align="middle">
      <el-col :span="16" :offset="3"><div class="el-col-16"></div></el-col>
      <el-col :span="8" :offset="16">
        <div class="aside">
          <div class="el-col-8"></div>
          <div class="el-col-8"></div>
          <div class="el-col-8"></div>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
    }
  },
  methods: {
    login () {
      console.log()
    }
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
  .el-col-16{
    height: 900px;
    width: 45%;
    background-color: aquamarine;
    z-index: 1;
  }
  .el-col-8{
    height: 300px;
    width: 335px;
    float: right;
    background-color: bisque;
  }
  .aside{
    height: 900px;
    width: 335px;
    position: fixed;
  }
</style>
