<template>
  <b-navbar toggleable="md" type="light" variant="default" fixed class="box">
    <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>
    <router-link to="/">
      <b-navbar-brand>
        <b-img width="85" height="50"
               src="../../static/img/logo.png"/>
      </b-navbar-brand>
    </router-link>

    <b-collapse is-nav id="nav_collapse">
      <b-navbar-nav>
        <b-nav-item v-if="user!=null">
          <router-link to="/">发现</router-link>
        </b-nav-item>
        <b-nav-item v-if="user!=null">
          <router-link to="/subscriptions">关注</router-link>
        </b-nav-item>
        <b-nav-item-dropdown right v-if="user!=null">
          <!-- Using button-content slot -->
          <template slot="button-content">
            <router-link to="/notifications">消息</router-link>
          </template>
          <b-dropdown-item>
            <router-link to="/notifications/comments">
              <i class="far fa-comment-alt" style="color: red"></i>&nbsp;&nbsp;评论
            </router-link>
          </b-dropdown-item>
          <b-dropdown-item>
            <router-link to="/notifications/chats">
              <i class="far fa-envelope" style="color: red"></i>&nbsp;&nbsp;简信
            </router-link>
          </b-dropdown-item>
          <b-dropdown-item>
            <router-link to="/notifications/requests">
              <i class="fas fa-upload" style="color: red"></i>&nbsp;&nbsp;投稿请求
            </router-link>
          </b-dropdown-item>
          <b-dropdown-item>
            <router-link to="/notifications/likes">
              <i class="far fa-heart" style="color: red"></i>&nbsp;&nbsp;喜欢和赞
            </router-link>
          </b-dropdown-item>
          <b-dropdown-item>
            <router-link to="/notifications/follows">
              <i class="fas fa-user-plus" style="color: red"></i>&nbsp;&nbsp;关注
            </router-link>
          </b-dropdown-item>
        </b-nav-item-dropdown>

        <b-nav-item v-if="user===null">
          <router-link to="/index">首页</router-link>
        </b-nav-item>

        <b-nav-item v-if="user===null">
          <router-link to="/download">下载APP</router-link>
        </b-nav-item>

        <b-nav-form>
          <b-form-input size="sm" class="mr-sm-2 search-input" type="text" placeholder="搜索"/>
          <font-awesome-icon icon="search" style="color: #999;font-size: 20px;margin-left: -50px;"/>
        </b-nav-form>
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
        <b-nav-item href="#">Aa</b-nav-item>
        <b-nav-item v-if="user===null">
          <router-link to="/sign_in">登录</router-link>
        </b-nav-item>

        <b-nav-item v-if="user===null">
          <router-link to="/sign_up">注册</router-link>
        </b-nav-item>
        <b-nav-item-dropdown right v-if="user!=null">
          <!-- Using button-content slot -->
          <b-dropdown-item>
            <router-link to="/u">
              <i class="fas fa-user" style="color: red"></i>&nbsp;&nbsp;我的主页
            </router-link>
          </b-dropdown-item>
          <b-dropdown-item>
            <router-link to="/settings">
              <i class="fas fa-cog" style="color: red"></i>&nbsp;&nbsp;设置
            </router-link>
          </b-dropdown-item>
          <template slot="button-content">
            <b-img rounded="circle" width="35" height="35" :src="user.avatar"/>
          </template>
          <b-dropdown-item @click="logout">
            <i class="fas fa-sign-out-alt" style="color: red"></i>&nbsp;&nbsp;退出
          </b-dropdown-item>
        </b-nav-item-dropdown>
        <a class="btn write-btn" href="/write">
          写文章
        </a>
      </b-navbar-nav>

    </b-collapse>
  </b-navbar>
</template>
<script>
  import 'bootstrap/dist/css/bootstrap.css'
  import 'jquery/dist/jquery.min'
  import 'bootstrap/dist/js/bootstrap.min'

  export default {
    data() {
      return {
        user: JSON.parse(localStorage.getItem('loginUser'))
      }
    },
    methods: {
      logout() {
        localStorage.removeItem('loginUser')
        this.$router.go(0);
      }
    }
  }
</script>
<style scoped>
  .box {
    border-bottom: 1px solid #eef1f6;
    height: 55px;
  }

  a {
    color: #324157;
  }

  .write-btn {
    float: right;
    width: 100px;
    height: 40px;
    line-height: 24px;
    margin: 8px 15px 0;
    border-radius: 20px;
    font-size: 15px;
    color: #fff;
    background-color: #ea6f5a;
  }

  .search-input {
    padding: 0 40px 0 20px;
    width: 160px;
    height: 38px;
    font-size: 14px;
    border: 1px solid #eee;
    border-radius: 40px;
    background: #eee;
  }
</style>
