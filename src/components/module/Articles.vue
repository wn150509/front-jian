<template>
    <div>
      <div class="row" v-for="article in articles" :key="article.articleId">
        <div class="col-md-8">
          <a :href=" '/p/'+article.articleId">
          <p v-text="article.articleTitle" class="title"></p>
          <p v-text="article.articleContent" class="content"></p>
          </a>
          <div>
            <span v-text="article.articleAuthor" class="nickname"></span>
            <span class="nickname"><i class="fas fa-comment-alt"></i>{{article.articleComment}}</span>
            <span class="nickname"><i class="fas fa-heart"></i>{{article.articleLike}}</span>
          </div><hr/>
        </div>
        <div class="col-md-4">
          <img v-bind:src="article.articlePic" class="picture"/>
        </div>
      </div>
    </div>
</template>

<script>
    export default {
      data(){
        return{
          articles:[]
        }
      },
      created(){
        var that=this
        this.$http
          .get('http://localhost:8080/articles/index')
          .then(function (response) {
            that.articles=response.data.data
          })
      }
    }
</script>

<style scoped>
.picture{
  width: 130px;
  height: 100px;
  margin-top: 20px;
}
  .title{
    font-size: 19px;
    font-weight: bold;
    margin-top: 15px;
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
