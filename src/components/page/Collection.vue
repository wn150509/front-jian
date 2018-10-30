<template>
  <div>
    <b-row>
      <b-col cols="8">
        <div class="main-top">
          <div class="avatar-collection">
            <img :src="topic.collections.collectionUrl" class="pic">
          </div>
          <a class="btn btn-success follow">
            <span>+关注</span>
          </a>
          <div class="btn btn-hollow js-contribute-button">
            投稿
          </div>
          <div class="title">
            <h3>{{topic.collections.collectionName}}</h3>
          </div>
          <div class="info">
            <p>
              <span>收藏了{{topic.collections.collectionArticle}}篇文章,{{topic.collections.collectionFans}}人关注。</span>
            </p>
          </div>
        </div><hr/>
        <!--专题文章-->
        <div class="row" v-for="article in topic.articlesList" :key="article.articleId">
          <div class="col-md-8">
            <a :href="'/p/'+article.articleId ">
              <p v-text="article.articleTitle" class="title"></p>
              <p v-text="article.articleContent" class="content"></p>
            </a>
            <span v-text="article.articleAuthor" class="nickname"></span>
            <span class="nickname"><i class="fas fa-comment-alt"></i>{{article.articleComment}}</span>
            <span class="nickname"><i class="fas fa-heart"></i>{{article.articleLike}}</span><hr/>
          </div>
          <div class="col-md-4">
            <img v-bind:src="article.articlePic" class="picture"/>
          </div>
        </div>
      </b-col>
      <b-col cols="4">
        <p class="greyFont">专题公告</p>
        <div class="discription">
          <p>{{topic.collections.collectionInfo}}</p><hr/>
          <p>
            <span class="greyFont">作者：{{topic.collections.collectionName}}</span>
          </p>
        </div><hr/>
        <div>
          <div class="title greyFont">关注的人</div>
          <div class="list" v-for="fans in topic.sysUserList" :key="fans.userId">
            <div>
              <a :href=" '/ou/'+fans.userId" class="avatar">
                <img v-bind:src="fans.avatar" v-b-tooltip.hover :title="fans.nickname">
              </a>
            </div>
          </div>
        </div>
      </b-col>
    </b-row>
  </div>

</template>

<script>
  export default {
    data() {
      return {
        id: this.$route.params.id,
        topic: {}
      }
    },
    created(){
      var that=this
      this.$http
        .get('http://localhost:8080/collections/c/'+that.id)
        .then(function (response) {
          that.topic=response.data.data
        })
    },
    activated() {
      this.id = this.$route.params.id;
    },
    computed: function () {
      return this.topic;
    }
  }
</script>

<style scoped>
  .picture{
    width: 130px;
    height: 100px;
  }
  .title{
    font-size: 19px;
    font-weight: bold;
    color: black;
  }
  .content{
    font-size: 15px;
    color: grey;
    overflow: hidden;
    text-overflow:ellipsis;
    white-space: nowrap;
  }
  .nickname{
    font-size: 11px;
    color: darkgray;
  }
  .main-top{
    margin-bottom: 35px;
    box-sizing: border-box;
    display: block;
  }
  .main-top .avatar-collection{
    float: left;
    width: 100px;
    height: 100px;
  }
  .avatar-collection{
    display: block;
    cursor: pointer;
  }
  .pic{
    width: 80px;
    height: 80px;
    border-radius: 10px;
  }
  .main-top .title{
    padding: 10px 0 0 100px;
  }
  .title{
    font-family: -apple-system,SF UI Display,Arial,PingFang SC,Hiragino Sans GB,Microsoft YaHei,WenQuanYi Micro Hei,
    sans-serif;
  }
  .main-top .info{
    margin-top: 10px;
    padding-left: 100px;
    font-size: 14px;
    color: #969696;
  }
  .main-top .follow{
    padding: 8px 0;
    width: 100px;
  }
  .main-top .btn{
    float: right;
    margin: 23px 0 23px 16px;
    font-size: 15px;
  }
  .follow{
    border-color: #42c02e;
    font-weight: 400;
    line-height: normal;
    padding: 8px 22px;
  }
  .btn-success{
    border-radius: 40px;
    color: #fff;
    background-color: #42c02e;
  }
  .btn{
    display: inline-block;
    text-align: center;
    vertical-align: center;
    touch-action: manipulation;
    cursor: pointer;
    border: 1px solid transparent;
    white-space: nowrap;
    user-select: none;
  }
  .main-top .btn-hollow{
    padding: 8px 0;
    width: 90px;
  }
  .btn-hollow{
    border:1px solid rgba(59,194,29,.7);
    color: #42c02e!important;
    font-weight: 400;
    line-height: normal;
    border-radius: 40px;
    background: none;
  }
  .greyFont{
    color: #969696;
  }
  .avatar img {
    border: 1px solid #ddd;
    border-radius: 50%;
    margin-left: -10px;
    width: 32px;
    height: 32px;
  }
  .list{
    float: left;
  }
</style>
