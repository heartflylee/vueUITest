<template>
  <form id="f-signUp" @submit.prevent="submit">
    <div class="s-input-box">
      <input type="text" class="input" placeholder="请输入手机号" v-model="user.phone"/>
    </div>
    <div class="s-input-box">
      <div class="box-captcha" id="popup-submit">
      </div>
    </div>
    <div class="s-input-box">
      <input type="text" class="input yzm-input" placeholder="请输入验证码"/>
      <a class="btn yzm-btn" href="javascript:void(0);">获取验证码</a>
    </div>
    <div class="s-input-box">
      <input type="password" class="input" placeholder="请输入密码" v-model="user.psw"/>
    </div>
    <div class="s-input-box">
      <input type="password" class="input" placeholder="请再次输入密码" v-model="user.rPsw"/>
    </div>
    <div class="s-input-box">
      <div class="checkbox">
        <label>
          <input type="checkbox" checked="checked" name="agree" id="agree">
          <i></i>同意《
          <a class="href" href="javascript:void(0)" @click="statement">云客法律声明及隐私权保护协议</a>
          》</label>
      </div>
    </div>
    <div class="s-input-box">
      <input type="submit" class="btn btn-primary signUp-submit" value="下一步"/>
    </div>
  </form>
</template>

<script type="text/ecmascript-6">
    export default {
        data (){
            return {
              user: {
                phone: "",
                psw: "",
                rPsw: ""
              }
            }
        },
      methods:{
        submit(event){
          var formData = JSON.stringify(this.user); // 这里才是你的表单数据
          console.log(formData);
          console.log('提交');
          //下一步
          this.$emit('submit',true)
          return false;
        },
        statement(){
            console.log("保护协议")
            this.$emit('statement',true)
        }
      }
    }
</script>

<style lang="scss" rel="stylesheet/scss">

</style>
