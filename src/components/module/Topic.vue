<template>
    <div class="t_collection">
      <a class="collection" v-for="topic in topics" :key="topic.collectionId">
        <a :href=" '/c/'+topic.collectionId ">
          <img v-bind:src="topic.collectionUrl" class="pic">
          <div class="tt" v-text="topic.collectionName"></div>
        </a>
      </a>
      <router-link to="/collections">
        <a style="color: lightslategrey">更多热门专题&nbsp;></a>
      </router-link>
    </div>
</template>

<script>
    export default {
      data(){
        return{
          topics:[]
        }
      },
      created(){
        var that=this
        this.$http
          .get('http://localhost:8080/collections/part')
          .then(function (response) {
            that.topics=response.data.data
          })
      }
    }
</script>

<style scoped>
  .t_collection{
  margin-bottom: 20px;
  }
  .tt{
    display: inline-block;
    color: black;
  }
  .collection {
    display: inline-block;
    margin: 0 18px 18px 0;
    min-height: 32px;
    background-color: #f7f7f7;
    border: 1px solid #dcdcdc;
    border-radius: 4px;
    vertical-align: top;
    overflow: hidden;
  }
  .pic{
    width: 35px;
    height: 35px;
  }
</style>
