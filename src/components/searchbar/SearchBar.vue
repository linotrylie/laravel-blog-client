<template>
    <div class="searchbar">
        <el-input placeholder="请输入内容" v-model="input" class="input-with-select">
            <el-button
                    slot="append"
                    icon="el-icon-search"
                    @click="search"
                    v-loading.fullscreen.lock="fullscreenLoading"
            >

            </el-button>
        </el-input>
    </div>
</template>

<script>
export default {
  name: 'app-searchbar',
  data () {
    return {
      fullscreenLoading: false,
      input: ''
    }
  },
  methods: {
    search () {
      this.fullscreenLoading = true
      setTimeout(() => {
        this.fullscreenLoading = false
      }, 2000)
    }
  }
}
</script>

<style scoped>
.searchbar{
    z-index: 990;
}
</style>
