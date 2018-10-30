<template>
    <div class="container person">
      <div class="row">
        <b-col cols="8">
          <div class="main-top">
            <div class="avatar-collection">
              <img :src="author.avatar">
            </div>
            <a class="btn btn-success follow">
              <span>+关注</span>
            </a>
            <div class="btn btn-hollow js-contribute-button">
              发简信
            </div>
            <div class="title">
              <h3>{{author.nickname}}</h3>
            </div>
            <div class="info">
              <ul>
                <li>
                  <div class="meta-block">
                    10<br/>
                    <span class="is">关注&nbsp;></span>
                  </div>
                </li>
                <li>
                  <div class="meta-block">
                    120<br/>
                    <span class="is">粉丝&nbsp;></span>
                  </div>
                </li>
                <li>
                  <div class="meta-block">
                    22<br/>
                    <span class="is">文章&nbsp;></span>
                  </div>
                </li>
                <li>
                  <div class="meta-block">
                    {{author.wordsCount}}k<br/>
                    <span class="is">字数&nbsp;></span>
                  </div>
                </li>
                <li>
                  <div class="meta-block">
                    {{author.likeCount}}k<br/>
                    <span class="is">收获喜欢&nbsp;></span>
                  </div>
                </li>
              </ul>
            </div>
          </div><br/><hr/>

          <div>
            <div class="row" v-for="article in works" :key="article.articleId">
              <div class="col-md-8">
                <router-link :to=" '/p/'+article.articleId ">
                  <p v-text="article.articleTitle" class="title"></p>
                  <p v-text="article.articleContent" class="content"></p>
                </router-link>
                <span class="nickname"><i class="fas fa-comment-alt"></i>{{article.articleComment}}</span>
                <span class="nickname"><i class="fas fa-heart"></i>{{article.articleLike}}</span><hr/>
              </div>
              <div class="col-md-4">
                <img v-bind:src="article.articlePic" class="picture"/>
              </div>
            </div>
          </div>

        </b-col>

        <b-col cols="4">
          <div>
            <img src="https://ws1.sinaimg.cn/large/00792MPDgy1fwfvktd36xj3080031q2t.jpg"/>
          </div><hr/>
          <p class="greyFont">个人介绍</p>
          <div class="discription">
            <p>{{author.description}}</p>
          </div><hr/>
          <div>
            <a>
              <img src="/static/img/网格.png" class="icon2"/>
              <span class="my">他关注的专题/文集/连载</span>
            </a><br/><br/>
            <a class="xia">
              <img src="/static/img/喜欢.png" class="icon3"/>
              <span class="my">他喜欢的文章</span>
            </a>
          </div><hr/>
        </b-col>
      </div>
    </div>
</template>

<script>
    export default {
      data() {
        return {
          id: this.$route.params.id,
          author: {},
          works:[]
        }
      },
      created(){
        var that=this
        this.$http
          .get('http://localhost:8080/articles/'+this.$route.params.id)
          .then(function (response) {
            that.works=response.data.data
          })
        this.$http
          .get('http://localhost:8080/user/'+this.$route.params.id)
          .then(function (response) {
            that.author=response.data.data
          })
      },
      activated() {
        this.id = this.$route.params.id;
      },
      computed: function () {
        return this.author;
      },
        name: "OtherUser"
    }
</script>
<style scoped>
  .my{
    margin-left: 8px;
  }
  .icon2{
    width: 26px;
    height: 26px;
  }
  .icon3{
    width: 26px;
    height: 26px;
  }
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
  .greyFont{
    color: #969696;
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
    margin-left: -40px;
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
  .avatar-collection img {
    width: 80px;
    height: 80px;
    border: 1px solid #ddd;
    border-radius: 50%;
    margin-left: -10px;
  }
  li{
    list-style-type: none;
  }
  .meta-block {
    float: left;
    font-size: 13px;
    margin: 0 7px 0 0;
    padding: 0 7px 0 0;
    border-right: 1px solid #f0f0f0;
  }
  .is{
    color: gray;
  }
</style>
