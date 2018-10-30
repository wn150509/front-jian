<template>
  <div>
    <b-row>
      <b-col cols="8" class="row">
        <!--左上-->
        <div class="main-top">
          <a class="avatar" >
            <img v-bind:src="user.avatar">
          </a>
          <div class="username">
            <a class="name">{{user.nickname}}</a>
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
                  {{user.wordsCount}}k<br/>
                  <span class="is">字数&nbsp;></span>
                </div>
              </li>
              <li>
                <div class="meta-block">
                  {{user.likeCount}}k<br/>
                  <span class="is">收获喜欢&nbsp;></span>
                </div>
              </li>
            </ul>
          </div>
        </div>
        <!--左下-->
        <div>
          <b-tabs class="zuoxia">
            <b-tab title="文 章" class="hh">
              <br>
              <div class="row" v-for="article in uarticles" :key="article.articleId">
                <div class="col-md-8">
                  <a :href="'/p/'+article.articleId ">
                  <p v-text="article.articleTitle" class="title"></p>
                  <p v-text="article.articleContent" class="content"></p>
                  </a>
                  <div>
                    <span class="nickname">
                      <i class="fas fa-comment-alt"></i>{{article.articleComment}}
                    </span>
                    <span class="nickname">
                      <i class="fas fa-heart"></i>{{article.articleLike}}
                    </span>
                  </div><hr/>
                </div>
                <div class="col-md-4">
                  <img v-bind:src="article.articlePic" class="picture"/>
                </div>
              </div>
            </b-tab>
            <b-tab title="动 态" class="hh">
              <br>
              <div class="row" v-for="article in uarticles" :key="article.articleId">
                <div class="col-md-8">
                  <a :href="'/p/'+article.articleId ">
                  <p v-text="article.articleTitle" class="title"></p>
                  <p v-text="article.articleContent" class="content"></p>
                  </a>
                  <div>
                    <span class="nickname">
                      <i class="fas fa-comment-alt"></i>{{article.articleComment}}
                    </span>
                    <span class="nickname">
                      <i class="fas fa-heart"></i>{{article.articleLike}}
                    </span>
                  </div><hr/>
                </div>
                <div class="col-md-4">
                  <img v-bind:src="article.articlePic" class="picture"/>
                </div>
              </div>
            </b-tab>
            <b-tab title="最 新 评 论" class="hh">
              <br>
              <div class="row" v-for="article in comments" :key="article.articleId">
                <div class="col-md-8">
                  <a :href="'/p/'+article.articleId ">
                  <p v-text="article.articleTitle" class="title"></p>
                  <p v-text="article.articleContent" class="content"></p>
                  </a>
                  <div>
                    <span class="nickname">
                      <i class="fas fa-comment-alt"></i>{{article.articleComment}}
                    </span>
                    <span class="nickname">
                      <i class="fas fa-heart"></i>{{article.articleLike}}
                    </span>
                  </div><hr/>
                </div>
                <div class="col-md-4">
                  <img v-bind:src="article.articlePic" class="picture"/>
                </div>
              </div>
            </b-tab>
            <b-tab title="热 门" class="hh">
              <br>
              <div class="row" v-for="article in likes" :key="article.articleId">
                <div class="col-md-8">
                  <a :href="'/p/'+article.articleId ">
                  <p v-text="article.articleTitle" class="title"></p>
                  <p v-text="article.articleContent" class="content"></p>
                  </a>
                  <div>
                    <span class="nickname">
                      <i class="fas fa-comment-alt"></i>{{article.articleComment}}
                    </span>
                    <span class="nickname">
                      <i class="fas fa-heart"></i>{{article.articleLike}}
                    </span>
                  </div><hr/>
                </div>
                <div class="col-md-4">
                  <img v-bind:src="article.articlePic" class="picture"/>
                </div>
              </div>
            </b-tab>
          </b-tabs>
        </div>
      </b-col>
      <!--右边-->
      <b-col cols="4" style="margin-top: 40px">
        <div>
          <span>个人介绍</span>
          <img src="/static/img/铅笔.png" class="icon1">
          <b-btn v-b-toggle.collapse1 variant="link" class="bj">编辑</b-btn>
          <b-collapse id="collapse1" class="mt-2">
            <b-card>
              <b-form-textarea id="textarea1"
                               v-model="text"
                               :rows="4"
                               :max-rows="4">
              </b-form-textarea>
            </b-card>
            <b-btn v-b-toggle.collapse1_inner variant="outline-success" class="bc">保存</b-btn>
            <b-btn v-b-toggle.collapse1 class="diss" variant="link">取消</b-btn>
          </b-collapse>
        </div><hr/>
        <div>
          <a>
            <img src="/static/img/网格.png" class="icon2"/>
            <span class="my">我关注的专题/文集/连载</span>
          </a><br/><br/>
          <a>
            <img src="/static/img/喜欢.png" class="icon3"/>
            <span class="my">我喜欢的文章</span>
          </a>
        </div><hr/>
        <div>
          <p class="wdzt">我创建的专题</p>
          <p class="cjzt">＋创建一个新专题</p>
        </div><hr/>
        <div>
          <p class="wdzt">我的文集</p>
          <a >
            <img src="/static/img/笔记.png" class="icon4">&nbsp;&nbsp;日记本
          </a>
        </div><hr/>
      </b-col>
    </b-row>
  </div>
</template>

<script>
  export default {
    name: "User",
    data(){
      return {
        user: JSON.parse(localStorage.getItem('loginUser')),
        uarticles:[],
        likes:[],
        comments:[]
      }
    }
    ,created(){
      var that=this
      this.$http
        .get('http://localhost:8080/articles/'+this.user.userId)
        .then(function (response) {
          that.uarticles=response.data.data
        })
      this.$http
        .get('http://localhost:8080/articles/ucomment/'+this.user.userId)
        .then(function (response) {
          that.comments=response.data.data
        })
      this.$http
        .get('http://localhost:8080/articles/ulike/'+this.user.userId)
        .then(function (response) {
          that.likes=response.data.data
        })
    }
  }
</script>

<style scoped>
  .wdzt{
    color: grey;
  }
  .cjzt{
    color: #50C050;
    font-size: 13px;
  }
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
  .icon4{
    width: 20px;
    height: 20px;
  }
  .bj{
    color: lightgray;
    font-size: 14px;
    margin-left: -18px;
  }
  .diss{
    color: lightgray;
  }
  .bc{
    height: 33px;
    width: 80px;
    border-radius: 15px;
  }
  .icon1{
    margin-left: 230px;
    width: 10px;
    height: 10px;
  }
  .avatar {
    float: left;
    width: 80px;
    height: 80px;
    margin-left: -2px;
    margin-top: 40px;
    display: block;
    cursor: pointer;
  }
  li{
    list-style-type: none;
  }
  .avatar img {
    width: 100%;
    height: 100%;
    border: 1px solid #ddd;
    border-radius: 50%;
  }
  .main-top {
    margin-bottom: 20px;
    float: left;
    position: relative;
    min-height: 1px;
    padding-left: 15px;
  }
  .username {
    margin-left: 200px;
    padding: 40px 0 0 0;
    margin-top: -5px;
  }
  .name {
    /*display: inline;*/
    font-size: 21px;
    font-weight: 700;
    margin-right: 300px;
    margin-left: -100px;
    margin-top: -5px;
    vertical-align: middle;
  }
  .info {
    padding-left: 60px;
    font-size: 14px;
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
  .zuoxia{
    width: 700px;
  }
  .hh{
    margin-left: 50px;
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
</style>
