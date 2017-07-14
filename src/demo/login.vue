<template>
  <div class="login-wrap">
    <div class="signIn-wrap" v-if="loginshow">
      <div class="s-logo"></div>
      <div class="s-main">
        <div class="login-box">
          <form @submit.prevent="login">
            <div class="input-box">
              <input type="text" class="input l-phone" placeholder="请输入手机号" v-model="user.phone"/>
            </div>
            <div class="input-box">
              <input type="password" class="input l-pwd" placeholder="请输入密码" v-model="user.psw"/>
            </div>
            <div class="input-box">
              <input type="submit" class="btn btn-primary l-submit" value="登 录"/>
            </div>
          </form>
        </div>
        <div class="l-bottom">
          <div class="right">
            <a class="a-btn" href="javascript:void(0)" @click="regist">注册</a>
            <a class="a-btn" href="javascript:void(0);">忘记密码</a>
            <div class="l-download">
              <label>下载云客APP</label>
              <div class="icon">
                <i class="android way-icon"></i>
                <div class="code-wrap">
                  <div class="code"></div>
                </div>
              </div>
              <div class="icon">
                <i class="ios way-icon"></i>
                <div class="code-wrap">
                  <div class="code"></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 注册弹框-->
    <transition name="layerShow">
      <layer-login v-if="signshow" title="欢迎注册云客企业版" name="signshow" @closelayer="closeSignLayer">
        <sign-up @submit="next" @statement="statement"></sign-up>
      </layer-login>
    </transition>
    <!-- 注册弹框-->

    <!-- 输入公司名称-->
    <transition name="layerShow">
      <layer-login v-if="comshow" title="欢迎注册云客企业版" name="comshow" @closelayer="closeSignLayer">
        <form @submit.prevent="company">
          <div class="s-input-box">
            <autocomplete id="company" classname="input" name="company" placeholder="请输入公司名称"
                          url="./static/data/company.json" param="value" limit="5" anchor="value"
                          @value="comValue"></autocomplete>
          </div>
          <div class="s-input-box">
            <input type="submit" class="btn btn-primary signUp-submit" value="完成注册"/>
          </div>
        </form>
      </layer-login>
    </transition>
    <!-- 输入公司名称-->

    <!-- 法律声明保护协议 -->
    <transition name="layerShow">
      <layer v-if="statementshow" :layer="statePara" @closelayer="closeStatement">
        <statement></statement>
      </layer>
    </transition>
    <!-- 法律声明保护协议 -->

    <!-- 企信信息-->
    <transition name="layerShow">
      <layer v-if="qixinshow">
        <qixin>
        </qixin>
      </layer>
    </transition>
    <!-- 企信信息-->
  </div>
</template>

<script>
  import '../js/beAlert.js'
  import layerLogin from  '../components/layerLogin/index.vue'
  import layer from '../components/layer/index.vue'
  import signUp from '../components/signUp/index.vue'
  import autocomplete from '../components/autocomplete/index.vue'
  import statement from '../components/statement/index.vue'
  import qixin from '../components/qixin/index.vue'

  export default {
    data(){
      return {
          loginshow:true,
        signshow: false,
        comshow: false,
        statementshow: false,
        qixinshow: false,
        user: {
          phone: "",
          psw: ""
        },
        statePara: {
          title: "云客法律声明及隐私权保护协议",
          submitBtn: false
        }
      }
    },
    components: {
      layerLogin,
      layer,
      signUp,
      autocomplete,
      statement,
      qixin
    },
    methods: {
      //显示注册弹框
      regist () {
        this.signshow = true
          this.loginshow = false
      },
      closeSignLayer(layer){
        console.log(this)
        console.log(this.$data[layer]);
        this.$data[layer] = !this.$data[layer]
        this.loginshow = true
      },
      closeLayer(){

      },
      //关闭注册弹框
//      closeSign(bool){
//        this.signshow = bool
//      },
//      //关闭输入公司名称弹框
//      closeCom(bool){
//        this.comshow = bool
//      },
      //保护协议显示
      statement(bool){
        console.log(bool)
        this.statementshow = bool
        this.signshow = false
      },
      //关闭保护协议
      closeStatement(bool){
        this.statementshow = bool
        this.signshow = true
      },

      next(){
        this.comshow = true
        this.signshow = false
      },

      company(){
        this.comshow = false
        this.loginshow = true
        console.log("注册完成")
      },
      //登陆跳转页面
      login(){
        if (this.user.phone == "") {
          alert("", "手机号不能为空", function () {

          });
          return false;
        }
        if (this.user.psw == "") {
          alert("", "密码不能为空", function () {

          });
          return false;
        }
        console.log(this.user);
        console.log("登陆");
        window.location.href = "/";
      },
      comValue(data){
        console.log(data);
      }
    }

  }
</script>

<style lang="scss" rel="stylesheet/scss">
  @import '../styles/reset.scss';
  @import '../styles/bootstrap.scss';
  @import '../styles/beAlert.scss';
  @import '../styles/component/common.scss';
  @import '../styles/component/bodyCommon.scss';

  .login-wrap {
    position: relative;
    height: 100%;
    background: url("../assets/login-bg.png");
    background-size: cover;
  }

  //登录
  .signIn-wrap {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate3d(-50%, -50%, 0);
  }

  .s-logo {
    height: 37px;
    margin-bottom: 24px;
    background-image: url("../assets/s-logo.png");
    background-repeat: no-repeat;
  }

  .s-main {
    width: 780px;
    padding: 25px;
    background: rgba(0, 0, 0, 0.5);
    border-radius: 8px;
  }

  .input-box {
    display: inline-block;
    margin-left: 20px;
    &:first-child {
      margin-left: 0;
    }
  }

  .l-phone {
    width: 320px;
  }

  .l-pwd {
    width: 190px;
  }

  .l-submit {
    width: 170px;
    height: 40px;
  }

  .l-bottom {
    margin-top: 21px;
    @include clearfix;
    color: #fff;

  }

  a.a-btn {
    display: inline-block;
    margin: 0 7px;
    text-decoration: underline;
    color: #fff;
  }

  .l-download {
    display: inline-block;
    margin-left: 15px;
    label {
      display: inline-block;
      margin-right: 10px;
    }
  }

  .code-wrap {
    position: absolute;
    display: none;
    top: 35px;
    left: 50%;
    padding: 10px;
    transform: translate3d(-50%, 0, 0);
    background: #fff;
    &:after {
      content: "";
      display: inline-block;
      position: absolute;
      top: -8px;
      left: 50%;
      transform: translate3d(-50%, 0, 0);
      @include triangle(top, 8px, #fff);
    }
    .icon:hover & {
      display: block;
    }
  }

  .code {
    @include icon;
    width: 152px;
    height: 152px;
    background-image: url("../assets/down-code.png");
    background-size: contain;
  }

  .icon {
    position: relative;
    display: inline-block;
    margin: 0 10px;
    //height: 20px;
    cursor: pointer;
    i {
      &:after {
        font-family: iconfont;
        font-style: normal;
        font-size: 25px;
        color: #fff;
        line-height: 1;
      }
      &.android:after {
        content: "\e655";
      }
      &.ios:after {
        content: "\e656";
      }
    }
  }

  /*@import "component/layer";*/

  .signUp-wrap {
    padding: 30px;
    background: #f5f5f5;
    &:before {
      content: "";
      position: absolute;
      top: 2px;
      left: 2px;
      bottom: 2px;
      right: 2px;
      border: 2px solid #252834;
    }
    .active & {
      animation-name: layerDown;
      animation-duration: 0.5s;
      animation-timing-function: ease-in-out;
    }
  }

  .signUp-close {
    position: absolute;
    top: 0;
    right: 0;
    width: 60px;
    height: 60px;
    text-align: center;
    line-height: 60px;
    overflow: hidden;
    cursor: pointer;
    &:before {
      content: "";
      position: absolute;
      z-index: 0;
      top: 0;
      left: 0;
      width: 200%;
      height: 100%;
      transform: rotate(45deg) translate3d(-26px, -8px, 0);
      background: #252834;
    }
    i {
      color: #fff;
      position: absolute;
      font-size: 35px;
      top: -7px;
      left: 30px;
    }
  }

  .signUp-main {
    padding: 10px 30px 20px;
  }

  .s-title {
    margin-bottom: 30px;
    text-align: center;
    font-size: 22px;
    font-weight: bold;
  }

  .s-box {
    width: 360px;
    margin: 0 auto;
  }

  .s-input-box {
    position: relative;
    margin-bottom: 20px;
  }

  .yzm-input {
    padding-right: 142px;
  }

  .yzm-btn {
    position: absolute;
    top: 5px;
    right: 8px;
    width: 120px;
    height: 32px;
    line-height: 32px;
    font-size: 12px;
    color: #fff;
    text-align: center;
    text-decoration: none;
    &.active {
      background: #d4d4d4;
      border-color: #d4d4d4;
      cursor: default;
    }
  }

  a.yzm-btn {
    color: #fff;
    text-decoration: none;
  }

  a.href {
    color: #50D2C2;
    text-decoration: none;
  }

  .signUp-submit {
    display: block;
    width: 100%;
    height: 40px;
  }

  .company-input {
    padding-right: 122px;
  }

  /*@import "./styles/component/qixin.scss";*/
  /*@import "./styles/component/statement.scss";*/

</style>
