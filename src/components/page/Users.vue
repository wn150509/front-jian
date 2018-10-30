<template>
  <div class="container">
    <img src="/static/img/zz.png" class="bt">
    <p class="rh">如何成为签约作者？</p>
    <div class="down">
      <div class="row">
        <div class="col-md-4" v-for="user in userList" :key="user.sysUser.userId">
          <b-card class="card">
              <a :href=" '/ou/'+user.sysUser.userId">
                <img v-bind:src="user.sysUser.avatar" class="pic">
                <p class="name">{{user.sysUser.nickname}}</p>
                <p class="title">{{user.sysUser.description}}</p>
              </a>
            <b-button size="size" variant="success">关注</b-button><hr>
            <p class="work">{{user.articlesList[0].articleTitle}}</p>
            <p class="work">{{user.articlesList[1].articleTitle}}</p>
            <p class="work">{{user.articlesList[2].articleTitle}}</p>
          </b-card>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
    export default {
        name: "Users",
      data(){
          return{
            userList:{}
          }
      },
      created(){
        var that=this;
        this.$http
          .get('http://localhost:8080/user/hotAll')
          .then(function (response) {
            that.userList=response.data.data
          })
      }
    }
</script>

<style scoped>
  .work{
    font-size: 13px;
    overflow: hidden;
    text-overflow:ellipsis;
    white-space: nowrap;
  }
  .bt{
    width: 1080px;
    height: 100px;
  }
  .name{
    font-size: 20px;
    color: black;
  }
  .title{
    color: #3C3C3C;
    overflow: hidden;
    text-overflow:ellipsis;
    white-space: nowrap;
  }
  .card{
    background-color: #EEEEEE;
  }
  .col-md-4 {
    text-align: center;
    float:left;
    margin-top: 80px;
  }
  .rh{
    margin-left: 780px;
    margin-top: -62px;
    color: white;
  }
  .down{
    margin-top: 50px;
  }
  .pic{
    width: 80px;
    height: 80px;
    border-radius: 50%;
    margin-top: -70px;
  }
</style>
