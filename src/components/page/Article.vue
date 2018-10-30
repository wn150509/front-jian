<template>
    <div class="row">
      <div class="col-md-2"></div>
      <div class="col-md-8">
        <h2>{{article.articleTitle}}</h2>
        <div class="author">
          <img :src="user.avatar" class="avatar"/>
          <span class="authorname">{{user.nickname}}</span>
          <span>
          <b-button size="sm" variant="success" class="gz">关注</b-button>
        </span>
          <div class="info">
            <span>{{article.createTime}}</span>
            <span>字数{{article.wordCount}}</span>
            <span>阅读{{article.lookCount}}</span>
            <span>评论{{article.articleComment}}</span>
            <span>喜欢{{article.articleLike}}</span>
          </div>
        </div>
        <div>
          <img v-bind:src="article.pic" class="picture"/>
          <p class="content">{{article.articleContent}}</p>
        </div>
        <div>
          <span class="pl">{{article.articleComment}}条评论</span>
          <span><b-button size="sm" variant="outline-secondary" class="zz">只看作者</b-button></span>
          <span class="px">按时间正序</span>
          <span>按时间倒序</span><hr/>
          <div v-for="comment in commentList" :key="comment.id">
            <div>
              <img :src="comment.userAvatar" class="userAvatar">
              <span class="usernick">{{comment.userNick}}</span>
              <span class="commenttime">{{comment.commentTime}}</span>
            </div>
            <div class="div2">
              <p>{{comment.commentContent}}</p>
            </div>
            <div>
              <span>赞</span>
              <span>回复</span>
            </div><hr/>
          </div>
        </div>
      </div>
      <div class="col-md-2"></div>
    </div>
</template>

<script>
    export default {
        name: "Article",
      data(){
          return{
            id:this.$route.params.id,
            article:{},
            user:{},
            commentList:[
              {
                'id':1,
                "userAvatar":"https://upload.jianshu.io/users/upload_avatars/14414923/3bf99397-971c-4e2c-915d-8b14926ac91d?imageMogr2/auto-orient/strip|imageView2/1/w/114/h/114",
                "userNick":"靈魂丶織舞",
                "commentContent":"理想中的爱情",
                "commentTime":"2018.10.21 12:51"
              },
              {
                'id':2,
                "userAvatar":"https://cdn2.jianshu.io/assets/default_avatar/9-cceda3cf5072bcdd77e8ca4f21c40998.jpg",
                "userNick":"海边的曼彻斯特q",
                "commentContent":"如果打算爱一个人，你要想清楚，是否愿意为了他，放弃如上帝般自由的心灵，从此心甘情愿有了羁绊。\n" +
                "不愿意\n" +
                "我们谁不是活在自己梦里的人 每时每刻",
                "commentTime":"2018.10.21 13:41 "
              }
            ]
          }
      },
      created(){
          var that =this
          this.$http
            .get('http://localhost:8080/articles/p/'+this.$route.params.id)
            .then(function (response) {
              that.article=response.data.data
            })
        this.$http
          .get('http://localhost:8080/user/p/'+this.$route.params.id)
          .then(function (response) {
            that.user=response.data.data
          })
      },
      activated(){
          this.id=this.$route.params.id;
      },
      computed: function () {
        return this.article;
      }
    }
</script>

<style scoped>
  .usernick{
    margin-left: 10px;
  }
  .commenttime{
    color: #969696;
    font-size: 12px;
    margin-left: 50px;
  }
  .userAvatar{
    width: 40px;
    height: 40px;
    border-radius: 50%;
  }
  .div2{
    margin-top: 10px;
  }
  .pl{
    font-weight: bold;
  }
  .px{
    margin-left: 400px;
  }
  .zz{
    border-radius: 20px;
    margin-left: 15px;
  }
  .content{
    margin-top: 30px;
  }
  .picture{
    width: 700px;
    height: 380px;
    margin-top: 35px;
  }
  .gz{
    width: 60px;
    height: 27px;
    border-radius: 10px;
    margin-top: -10px;
  }
  .author{
    margin-top: 30px;
    margin-left: 125px;
  }
  h2{
    text-align: center;
  }
  .avatar{
    width: 50px;
    height: 50px;
    border-radius: 50%;
  }
  .authorname{
    font-size: 20px;
    margin-left: 10px;
  }
  .info{
    margin-left:65px ;
    margin-top: -20px;
  }
  .info span{
    font-size: 13px;
    color: slategray;
  }
</style>
