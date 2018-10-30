<template>
  <div class="sign">
    <div class="logo">
      <a href="/">
        <img src="/static/img/logo.png">
      </a>
    </div>
    <div class="main">
      <h4 class="title">
        <div class="normal-title">
          <a class="active" href="/sign_in">
            <span class="red">登录</span>
          </a>
          <b>·</b>
          <a id="js-sign-up-btn" class="register" href="/sign_up">注册</a>
        </div>
      </h4>
      <div class="js-sign-in-container">
        <form id="new_session" action="/sessions" accept-charset="UTF-8" method="post">
          <input name="utf8" type="hidden" value="✓">
          <input type="hidden" name="authenticity_token" value="5RK+HVp8if7enNxRWV5Pb1FyPQxP/hGZafuWVG7FTC/r25fM/OaBTUOfvjq4KRQ1MmSxgPf437fPiFvCTV7Odw==">

          <!-- 正常登录登录名输入框 -->
          <div class="demo-input-suffix">
            <el-input
              placeholder="手机号或邮箱"
              prefix-icon="el-icon-yonghu"
              required
              v-model="email">
            </el-input>
          </div>

          <div class="demo-input-suffix">
            <el-input
              type="password"
              placeholder="密码"
              prefix-icon="el-icon-mima"
              required
              v-model="password">
            </el-input>
          </div>

          <div class="remember-btn">
            <input type="checkbox" value="true" checked="checked" name="session[remember_me]" id="session_remember_me">
            <span class="word">记住我</span>
          </div>

          <div class="forget-btn">
            <b-dropdown id="ddown-buttons" text="登录遇到问题?" variant="link" class="m-2 dropcolor ">
              <b-dropdown-item-button>用手机号重置密码</b-dropdown-item-button>
              <b-dropdown-item-button>用邮箱重置密码</b-dropdown-item-button>
              <b-dropdown-item-button>无法用海外手机号登录</b-dropdown-item-button>
              <b-dropdown-item-button>无法用 Google 帐号登录</b-dropdown-item-button>
            </b-dropdown>
          </div>

          <button class="sign-in-button" id="sign-in-form-submit-btn" type="button" @click="onClick">
            <span id="sign-in-loading"></span>登录
          </button>
        </form>
        <!-- 更多登录方式 -->
        <div class="more-sign">
          <h6>
            社交帐号登录
          </h6>
          <ul>
            <li id="weibo-link-wrap" class="">
              <a class="weibo" id="weibo-link">
                <img src="/static/img/微博.png"/>
              </a>
            </li>
            <li>
              <a id="weixin" class="weixin" target="_blank">
                <img src="/static/img/微信.png">
              </a>
            </li>
            <li>
              <a id="qq" class="qq" target="_blank">
                <img src="/static/img/qq.png"/>
            </a>
            </li>
            <li>
              <a class="douban" target="_blank">
                <img src="/static/img/豆瓣.png"/>
              </a>
            </li>
          </ul>
      </div>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        email: '',
        password: ''
      }
    },
    methods: {
      onClick() {
        var that = this;
        this.$http
          .post('http://localhost:8080/user/sign_in',
                {"email": this.email,
                "password": this.password})
          .then(function (response) {
            //alert(JSON.stringify(response.data.data));
            localStorage.setItem("loginUser", JSON.stringify(response.data.data))
            that.$router.push("/")
          })
      }
    }
  }
</script>

<style scoped>
  .sign {
    height: 100%;
    min-height: 750px;
    text-align: center;
    font-size: 14px;
    background-color: #f1f1f1;
    color: gray;

  }

  .red{
    color: #ea6f5a;
  }
  .logo {
    position: absolute;
    top: 56px;
    margin-left: 50px;
  }
  .sign .reset-title a, .sign .title a {
    padding: 10px;
    color: #969696;
  }
  .main {
    width: 400px;
    margin: 100px auto 0;
    padding: 50px 50px 30px;
    background-color: #fff;
    border-radius: 4px;
    box-shadow: 0 0 8px rgba(0,0,0,.1);
    vertical-align: middle;
    display: inline-block;
  }
   .title {
    font-family: -apple-system,SF UI Display,Arial,PingFang SC,Hiragino Sans GB,Microsoft YaHei,WenQuanYi Micro Hei,sans-serif;
    margin: 0 auto 50px;
    padding: 10px;
    font-weight: 400;
    color: #969696;
  }
  .active {
    font-weight: 700;
    color: #ea6f5a;
    border-bottom: 2px solid #ea6f5a;
    font-size: 20px;
  }

  .register{
    font-size: 20px;
  }
  form {
    margin-bottom: 30px;
  }
  .word{
    color: RGB(150,150,150);
  }
  .remember-btn {
    float: left;
    margin: 30px 0 ;
  }
  .forget-btn {
    float: right;
    position: relative;
    margin: 15px 0;
    font-size: 14px;
  }
  .more-sign {
    margin-top: 50px;
  }

  .sign-in-button {
    background: #3194d0;
    margin-top: 20px;
    width: 100%;
    padding: 9px 18px;
    font-size: 18px;
    border: none;
    border-radius: 25px;
    color: #fff;
    cursor: pointer;
    outline: none;
    display: block;
    clear: both;
  }
  .sign .more-sign h6 {
    position: relative;
    margin: 0 0 10px;
    font-size: 12px;
    color: #b5b5b5;
    font-family: inherit;
    font-weight: 500;
    line-height: 1.1;
  }

  h6::before {
    content: "";
    border-top: 1px solid #b5b5b5;
    display: block;
    position: absolute;
    width: 60px;
    top: 5px;
    left: 30px;
    box-sizing: border-box;
  }

  h6::after{
    content: "";
    border-top: 1px solid #b5b5b5;
    display: block;
    position: absolute;
    width: 60px;
    top: 5px;
    right: 30px;
    box-sizing: border-box;
  }
  .sign .more-sign ul {
    margin-bottom: 10px;
    list-style: none;
    padding-left: 0;
    margin-top: 0;
    display: block;
  }
  .sign .more-sign ul li {
    margin: 0 5px;
    display: inline-block;
    line-height: 20px;
    text-align: -webkit-match-parent;
  }
  .sign .more-sign ul a {
    width: 50px;
    height: 50px;
    line-height: 50px;
    display: block;
    cursor: pointer;
  }
  .qq{
    width: 50px;
    height: 50px;
    line-height: 50px;
    display: block;
    cursor: pointer;
  }
</style>

