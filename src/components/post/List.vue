<template>
<div class="post-list">
    <el-row class="art-item" v-for="post in lists" align="center" :key="post.id">
        <el-card shadow="hover">
            <div class="top">
                <i class="el-icon-top" v-if="post.sort" style="font-size: 24px;">置顶</i>
            </div>
            <h5><router-link :to="{name:'Article',query:{postId:post.id}}" tag="span" class="art-title">{{post.title}}</router-link></h5>
            <el-row class="art-info d-flex align-items-center justify-content-start">
                <div class="art-time"><i class="el-icon-time"></i>：{{post.created_at}}</div>
                <div class="d-flex align-items-center">
                    <!--<img class="tag" src="" />：-->
                </div>
            </el-row>
            <el-row class="art-body">
                <div class="side-img hidden-sm-and-down">
                    <div v-if="post.banner">
                        <img class="art-banner" :src="post.banner">
                    </div>
                    <div v-else>
                        <img class="art-banner" src="../../assets/1.jpg">
                    </div>
                </div>
                <div class="side-abstract">
                    <div class="art-abstract" v-html="post.text">
                    </div>
                    <div class="art-more">
                        <el-button plain @click="toArticle(post.id)">阅读全文</el-button>
                        <div class="view"><i class="el-icon-view"></i>{{ post.views }}</div>
                        <div class="view"><i class="el-icon-chat-dot-round"></i>{{ post.comments }}</div>
                        <div class="view"><i class="el-icon-position"></i>{{ post.shares }}</div>
                        <div class="view"><i class="el-icon-star-off"></i>{{ post.follows }}</div>
                    </div>
                </div>
            </el-row>

        </el-card>
    </el-row>
    <div class="block pagination">
        <el-pagination
                @size-change="handlePageSizeChange"
                @current-change="handleCurrentPageChange"
                :current-page="meta.pagination.current_page"
                layout="total, sizes, prev, pager, next, jumper"
                :total="meta.pagination.total"

        >
        </el-pagination>
    </div>
</div>
</template>

<script>
export default {
  name: 'post-list',
  props: ['data'],
  data () {
    return {
      pageData: {
        page: 1,
        page_size: 10
      },
      lists: {},
      meta: {}
    }
  },
  methods: {
    loadPost () {
      this.$http.get('http://laravel-blog-server.com/home/posts_list?page_size=' + this.pageData.page_size + '&page=' + this.pageData.page)
        .then(response => {
          this.lists = response.data.data.data
          this.meta = response.data.data.meta
          console.log(this.meta)
        })
        .catch(err => {
          console.log(err)
        })
    },
    handleCurrentPageChange (selectedPageNo) {
      this.meta.pagination.page = selectedPageNo
      // 下面的事件解释如上
      this.load(this.pageData.page_size, this.meta.pagination.page)
    },
    handlePageSizeChange (selectedPageSize) {
      this.pageData.page_size = selectedPageSize
      // 下面是改变了页面展示条数，需要马上触发的事件，如页面展示的一些记录，如果改变了每页展示的条数，也需要马上获取后台的数据
      this.load(this.pageData.page_size, this.meta.pagination.page)
    },
    load (pageSize, page) {
      console.log(pageSize)
      console.log(page)
      this.$http.get('http://laravel-blog-server.com/home/posts_list?page_size=' + pageSize + '&page=' + page)
        .then(response => {
          this.lists = response.data.data.data
          this.meta = response.data.data.meta
        })
        .catch(err => {
          console.log(err)
        })
    },
    toArticle (id) {
      console.log(id)
      this.$router.push({path: '/article', query: {postId: id}})
    }
  },
  mounted () {
    let that = this
    that.loadPost()
  }
}
</script>

<style scoped>
    #side .item {
        margin-bottom: 30px;
    }

    .art-item {
        margin-bottom: 30px;
        position: relative;
    }

    .art-item .star {
        width: 60px;
        height: 60px;
        position: absolute;
        top: 0;
        right: 0;
    }

    img.tag {
        width: 16px;
        height: 16px;
    }
    .star{
        width: 50px;
        height: 50px;
    }
    .art-title {
        border-left: 3px solid #F56C6C;
        padding-left: 5px;
        cursor: pointer;
    }

    .art-title:hover {
        padding-left: 10px;
        color: #409EFF;
    }

    .art-time {
        margin-right: 20px;
    }

    .art-body {
        display: flex;
        padding: 10px 0;
    }

    .side-img {
        height: 150px;
        width: 270px;
        overflow: hidden;
        margin-right: 10px;
    }

    img.art-banner {
        width: 100%;
        height: 100%;
        border-radius: 10px;
        transition: all 0.6s;
    }

    img.art-banner:hover {
        transform: scale(1.4);
    }

    .side-abstract {
        flex: 1;
        display: flex;
        flex-direction: column;
    }

    .art-abstract {
        flex: 1;
        color: #aaa;
        text-align: left;
    }

    .art-more {
        height: 40px;
        display: flex;
        justify-content: space-between;
        align-items: flex-end;
    }

    .art-more .view {
        color: #aaa;
    }
    h5{
        font-size: 18px;
    }
    .pagination {
        background-color: #F9F9F9;
    }
    .top{
        float: right;
    }
</style>
