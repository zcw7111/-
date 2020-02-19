<template>
<div>
  <div class="lg">
    <div class="login" v-show="!showR">
      <div class="head">
        <span @click="cancel">取消</span>
        <h4>登录</h4>
      </div>
      <div class="phone">
        <i></i>
        <mt-field v-model="phone" placeholder="请输入手机号"></mt-field>
      </div>
      <div class="pwd">
        <i></i>
        <mt-field v-model.trim="upwd" placeholder="请输入密码" type="password"></mt-field>
      </div>
      <button @click="login">登录</button>
      <p>
        登录即代表你同意<span>《服务协议》</span>和<span>《隐私政策》</span>
        <span class="Lreg" @click="reg">注册</span>
      </p>
    </div>
    <div class="reg" v-show="showR">
      <div class="head">
        <span @click="cancel">取消</span>
        <h4>注册</h4>
      </div>
      <div class="phone">
        <i></i>
        <mt-field v-model="rphone" placeholder="请输入手机号" v-on:input="changeR"></mt-field>
      </div>
      <div class="pwd">
        <i></i>
        <mt-field v-model.trim="rpwd" placeholder="请输入密码" type="password" v-on:input="changeR"></mt-field>
      </div>
      <p class="msg">提示：密码应包含大小写字母及数字，不能有特殊符号</p>
      <div class="cpwd">
        <i></i>
        <mt-field v-model="cpwd" placeholder="请确认密码" type="password" v-on:input="changeR"></mt-field>
      </div>
      <button @click="Yreg">注册</button>
      <p>
        已阅读并同意<span>《用户注册协议》</span>
      </p>
    </div>
  </div></div>
</template>
<script>
export default {
  data() {
    return {
      phone:"",
      rphone:"",
      upwd:"",
      rpwd:"",
      cpwd:"",
      showR:false,
    }
  },
  beforeCreate:function() {
    $("body")[0].style.background="#fff"
  },
  beforeDestroy:function(){
    $("body")[0].style.backgroundImage="-webkit-linear-gradient(top,#f3fbcc,#afe471)"
  },
  methods: {
    login(){
      var phone=this.phone;
      var upwd=this.upwd;
      if(!upwd){
        this.$toast("密码不能为空");
        return
      }
      var url="login";
      var obj={phone:phone,upwd:upwd};
      this.axios.get(url,{params:obj}).then(res=>{//成功回调函数
        //8：获取服务器返回结果
        if(res.data.code==2){
            this.$toast("已登录");
            return
        }
        if(res.data.code==-1){
          //9：出错显示出错信息
          this.$messagebox("用户名或密码有误！")
        }else{
          this.$router.go(-1)
        }
      })
    },
    cancel(){
     this.$router.go(-1)
    },
    reg(){
      this.showR=true
    },
    Yreg(){
      var reg=/^1[3-9]\d{9}$/;
      var regPwd=/^(?![0-9a-z]+$)(?![A-Za-z]+$)[0-9A-Za-z]+$/; //至少包含一位大写字母、一位数字，不能有特殊符号
      var rphone=this.rphone;
      var rpwd=this.rpwd;
      var cpwd=this.cpwd;
      if(!reg.test(rphone)){
        this.$toast("手机号格式不正确");
        return
      }
      if(!regPwd.test(rpwd)){
        this.$toast("密码格式不正确");
        return
      }
      if(rpwd!==cpwd){
        this.$toast("两次密码不相同");
        return
      }
      if(reg.test(rphone)&&regPwd.test(rpwd)&&rpwd==cpwd){
        var url="reg";
        var obj={phone:this.rphone,upwd:this.rpwd}
        this.axios(url,{params:obj}).then(res=>{
          if(res.data.code==1){
            this.$toast("注册成功")
            this.showR=false
          }else if(res.data.code==-1){
            this.$toast("该用户已存在")
          }
        })
      }
    },
    changeR(){
      var reg=/^1[3-9]\d{9}$/;
      var regPwd=/^(?![0-9a-z]+$)(?![A-Za-z]+$)[0-9A-Za-z]+$/; //至少包含一位大写字母、一位数字，不能有特殊符号
      var rphone=this.rphone;
      var rpwd=this.rpwd;
      var cpwd=this.cpwd;
      if(reg.test(rphone)&&regPwd.test(rpwd)&&rpwd==cpwd){
        var btn=document.querySelector(".reg button")
        btn.style.background="#2bc14c";
      }
    }
  }
}
</script>
<style scoped>
  .lg{
    width: 90%;
    margin: 1rem auto;
    box-shadow: 3px 5px 11px 1px #b0b6bc;
    border-radius: 5px;
    border: #9c9c9c
  }
  .login,.reg{
    padding: 1.2rem .8rem;
  }
  .login>div,.reg>div{
    display: flex;
    /* margin-bottom: 1rem; */
  }
  .lg .phone{
    margin-bottom: 0;
  }
  .head span{
    color: #138d18;
    font-size: .9rem
  }
  .head h4{
    margin: 0 auto;
  }
  .login i{
    background: url(../../assets/phone.png) no-repeat;
    background-size: 100%;
    display: block;
    width: 25px;
    height: 25px;
    position: relative;
    top: .7rem;
  }
  .pwd i{
    background: url(../../assets/password.png) no-repeat;
    background-size: 100%;
  }
  .reg i{
    background: url(../../assets/password.png) no-repeat;
    background-size: 100%;
    display: block;
    width: 25px;
    height: 25px;
    position: relative;
    top: .7rem;
  }
  .phone i{
    background: url(../../assets/phone.png) no-repeat;
    background-size: 100%;
  }
  .login >>> .mint-cell,.reg >>> .mint-cell{
    width: 100%;
  }
  button{
    width: 100%;
    border: 0;
    border-radius: 1.2rem;
    padding: .65rem 0;
    color: #fff;
    margin-top: .9rem;
  }
  p{
    margin-top: 1.6rem;
    color: #9c9c9c;
    font-size: .7rem
  }
  p span{
    color: #33b938
  }
  p span.Lreg{
    float: right;
  }
  .reg .msg{
    color: #e46363;
    margin:.7rem 0
  }
</style>