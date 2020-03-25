<template>
    <div>
        <el-row class="main">
            <el-col :span="16" :offset="4">
                <div id="artcle-info">
                    <h2 class="text-center"><strong>{{post.title}}</strong></h2>
                    <!-- 描述：文章信息 -->
                    <div class="text-center timeAndView">
						<span class="article-time">
							<i class="el-icon-time"></i>
							发表于：<span>{{post.created_at}}</span>
						</span>
                        &nbsp;|&nbsp;
                        <span class="article-views">
							<i class="el-icon-view"></i>
							阅读量：<span>{{post.views}}</span>
						</span>
                    </div>
                </div>
                <hr />
                <div class="entry-content">
                    <div v-html="post.text"></div>
                </div>
                <br>
                <div id="statement">
                    <div class="item">作者:{{post.auth_name}}</div>
                    <div class="item">原文链接：
                        <a href="https://www.pling.top">https://www.pling.top</a>
                    </div>
                    <div class="item">Linotrylie：本博客所有文章除特别声明外,转载请注明出处!</div>
                </div>
            </el-col>
        </el-row>
    </div>
</template>

<script>
export default {
  name: 'Article',
  data () {
    return {
      post_id: this.$route.query.postId,
      post: {}
    }
  },
  methods: {
    loadPost (post_id) {
      if (!post_id) {
        this.$notify({
          title: '提示信息',
          message: '信息不符合规则！',
          type: 'error'
        })
        return false
      }
      this.$http.get('http://laravel-blog-server.com/home/post_info?post_id=' + post_id)
        .then(response => {
          this.post = response.data.data
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
    that.loadPost(that.post_id)
  }
}
</script>

<style scoped>
    #artcle-info {
        padding: 20px;
        background-image: url(../../assets/1.jpg);
        margin-bottom: 40px;
    }
    #artcle-info .timeAndView {
        padding: 20px;
        line-height: 30px;
        font-size: 16px;
        color: #ffffff;
    }

    pre {
        color: #ffffff;
        background-color: rgba(0, 0, 0, 0.8);
    }

    img{
        width: 100%;
    }
    .text-center {
        color:#fff;
    }
    #statement {
        border-left: 3px solid #F56C6C;
        padding: 20px;
        background-color: #EBEEF5;
    }
    .entry-content ul {
        list-style: disc;
        padding: 5px 10px 5px 50px;
        color: #828282;
        margin-left: 0;
        border: 1px solid #ddd;
        border-radius: 5px;
    }

    .entry-content ol {
        list-style: decimal;
        padding: 5px 10px 5px 50px;
        color: #828282;
        margin-left: 0;
        border: 1px solid #ddd;
        border-radius: 5px;
    }

    .entry-content ol li , .entry-content ul li {
        padding: 15px 0;
        border-top: 1px solid #ddd;
    }

    .entry-content ol li:first-child , .entry-content ul li:first-child {
        border-top: none;
    }

    .entry-content {
        position: relative;
        text-align: left;
    }

    .entry-content h2 {
        color: #737373;
        font-size: 20px;
    }
    .entry-content h2:before {
        content: "[";
        margin-right: 5px;
        color: #ff6d6d;
        font-size: 25px;
    }
    .entry-content h2:after {
        content: "]";
        margin-left: 5px;
        color: #ff6d6d;
        font-size: 25px;
    }

    .entry-content h3 {
        color: #6d6c6c;
        background: #F9F9F9;
        padding: 10px 0 10px 20px;
        border-left: 5px solid #C4E2EA;
        font-weight: normal;
        font-size: 16px;
        border-radius: 3px;
    }

    .entry-content h4 , .entry-content h5 {
        padding: 20px 35px;
        background: #FFF6B5;
        color: #737373;
        font-weight: normal;
        border-radius: 3px;
        position:relative;
        padding-left:60px;
        box-shadow: 0 2px 3px rgba(0,0,0,.06);
    }

    .entry-content h5 {
        font-size: 16px;
        background: #C8E6FB;
    }

    .entry-content h4:before , .entry-content h5:before{
        font-family: 'iconfont';
        font-size: 25px;
        content: "\e60b";
        color: #C7BF83;
        margin-right: 10px;
        position: absolute;
        left: 20px;
        top: 16px;
    }

    .entry-content h5:before {
        content: "\e605";
        color: #7C9AAF;
    }

    .entry-content code {
        background: #f9f9f9;
        color: #E67474;
        padding: 2px 4px;
        border-radius: 2px;
    }

    .entry-content a {
        color: #E67474;
        text-decoration: underline;
    }

    .entry-content a:hover {
        color: #72C5A6;
    }


    h1.entry-title {
        font-size: 22px;
        font-weight: 300;
    }

    .entry-content p{
        color: #565656;
        font-weight: 400;
    }

    .entry-content p{
        line-height:30px
    }

    .entry-content:before,
    .entry-content:after{
        content: "";
        display: table;
        table-layout: fixed;
    }

    .entry-content:after {
        clear: both;
    }
</style>
