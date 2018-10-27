<template>
    <div class="container">
      <img src="https://cdn2.jianshu.io/assets/web/recommend-collection-58f8968955ecbeb8f8f3b4cd95ec76be.png"
      class="bt">
      <p class="rh">如何创建并玩转专题？</p>
      <div class="down">
        <b-tabs>
          <b-tab title=" 推荐" active>
            <br>
            <div class="row">
              <div class="col-md-4" v-for="topic in topicList" :key="topic.collectionId">
                <b-card class="card">
                  <a :href=" '/c/'+topic.collectionId ">
                    <img v-bind:src="topic.collectionUrl" class="pic">
                    <p class="name">{{topic.collectionName}}</p>
                    <p class="title">{{topic.collectionInfo}}</p>
                  </a>
                  <b-button size="size" variant="success">关注</b-button>
                  <hr>
                  <span>{{topic.collectionArticle}}篇文章</span>
                  <span> · {{topic.collectonFans}}k人关注</span>
                </b-card>
              </div>
            </div>
          </b-tab>

          <b-tab title=" 热门" >
            <br>热门
          </b-tab>
          <b-tab title=" 城市">
            <br>城市
          </b-tab>
          <b-tab title=" 校园">
            <br>校园
          </b-tab>
        </b-tabs>
      </div>

    </div>
</template>

<script>
    export default {
        name: "Collections",
      data(){
          return{
            topicList:[]
          }
      },
      created(){
        var that=this
        this.$http
          .get('http://localhost:8080/collections/all')
          .then(function (response) {
            that.topicList=response.data.data
          })
      }
    }
</script>

<style scoped>
  .name{
    font-size: 20px;
    color: black;
  }
  .title{
    color: #3C3C3C;
  }
  .col-md-4 {
    text-align: center;
    float:left;
    margin-top: 80px;
  }
  .card{
    background-color: #EEEEEE;
  }
  .pic{
    width: 80px;
    height: 80px;
    border-radius: 10px;
    margin-top: -70px;
  }
  .down{
    margin-top: 80px;
  }
  .bt{
    width: 960px;
    height: 100px;
  }
  .rh{
    margin-left: 780px;
    margin-top: -62px;
    color: white;
  }
</style>
