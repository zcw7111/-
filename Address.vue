<template>
  <div class="addAddress">
    <div class="main">
        <div class="top">添加收货地址 <i @click="close">×</i></div>
        <div class="inp">
          <input type="text" v-model="name" placeholder="收货姓名" @blur="bName" class="xm"
          :style="{webkitTextFillColor:(name==''?'#d2d2d2':'#151516')}"><input type="text" v-model="phone" placeholder="手机号码" @blur="bPhone" class="sj" :style="{webkitTextFillColor:(phone==''?'#d2d2d2':'#151516')}">
        </div>
        <div class="center" @click="choose">
          <span>选择地区</span><i class="dayu"></i>
        </div>
        <div class="bottom">
          <textarea type="text" v-model="address" placeholder="详细地址(如街道、小区、乡镇、村)" class="dz" @blur="bAddress" :style="{webkitTextFillColor:(address==''?'#d2d2d2':'#151516')}"></textarea>
          <div class="position-ico"></div>
        </div>
        <div class="btn" @click="save" :style="{opacity:c!='选择地区'&&name&&phone&&address?'1':'.2'}">
          <span>保存</span>
        </div>
    </div>
    <div class="content">
      <div class="bg"></div>
      <v-distpicker type="mobile" @selected="sel"></v-distpicker>
    </div>
  </div>
</template>
<script>
import VDistpicker from 'v-distpicker'
export default {
  data(){
    return{

      name:"",
      phone:"",
      address:"",
      a:1,
      pay:false,
      a:false,
      c:"选择地区"
    }
  },

  name:"demo",
  components: { VDistpicker },
  Destroy(){
    this.cancel();
  },
  props:{
    uid:""
  },
  methods:{
    sel: function(data) {
      this.citydata = data.province.value+" "+ data.city.value+" " + data.area.value;
      this.c=this.citydata
      $(".center span").html(this.citydata);
      this.cancel();
    },
    bName(){
      console.log(this.uid)
      if(this.name==""){
        this.$toast("请填写收货姓名");
        return
      }
    },
    bPhone(){
      var reg=/^1[3-9]\d{9}$/;
      var phone=this.phone;
      if(phone==""){
        this.$toast("请填写手机号码");
        return
      }else{
        if(!reg.test(phone)){
          this.$toast("请填写正确的手机号码");
          $(".sj").css("-webkit-textFill-color","red")
          return
        }else{
          $(".sj").css("-webkit-textFill-color","#151516")
          return 1
        }
      }
    },
    bAddress(){
      if(this.address==""){
        this.$toast("请填写详细地址")
        return
      }else{
        return 1
      }
    },
    save(){
      if(!this.name){
        return
      }else if(!this.bPhone()){
        return
      }else if(!this.bAddress()){
        return
      }else if(this.c=="选择地区"){
        this.choose()
        return
      }else{
        var url="addaddress";
        var add=this.c+" "+this.address;
        var obj={uid:this.uid,receiver:this.name,address:add,cellphone:this.phone,group:1};
        this.axios.get(url,{params:obj})
        this.$toast("添加成功");
        this.close();
        parent.location.reload()
      }
    },
    close(){
      this.$emit('func',this.pay)
    },
    choose(){
      $(".content").css("display","block")
      setTimeout(function(){
        $(".distpicker-address-wrapper").css("transform","translateY(0rem)")
      },1);
      $(".address-header").prepend($("<span class='hi' >取消</span>"))
        $(".address-header>span").click(()=>{
          this.cancel()
        })
    },  
    cancel(){
      $(".distpicker-address-wrapper").css("transform","translateY(25rem)")
      setTimeout(function(){  $(".content").css("display","none") },500);
      $(".address-header>span").remove();
    }
  }
}
</script>
<style scoped>
  .addAddress{
    height: 100%;
    position: fixed;
    background: rgba(0,0,0,.7);
    top:0;
    width: 100%;
    z-index: 1000;
  }
  .main{
    position: absolute;
    top:20%;
    left:5%;
    width: 90%; 
    border-radius:6px;
    background-color: #fff;
    color: #151516;
  }
  .top{
    text-align: center;
    padding: .82rem 0;
    font-size:1.1rem;
    width: 100%;
    border-bottom: 1px solid #ededed;  
  }
  .top i{
    font-size:1.6rem;
    padding: 1.125rem   .875rem;
    color:#ddd;
    position: absolute;
    top:-3%;
    right: 0;
  }
  .inp{
    width: 100%;
    text-align: left;
  }
  .inp>input{
    width: 50%;
    outline: 0;
    border-radius:0; 
    border-left:0 ;
    border-top: 0;
    border-bottom: 0;
    border-right:1px solid #ededed; 
    padding:.625rem 0 .625rem .875rem ;
    font-size:.9rem;
    display:inline-block;
    height:2.8125rem ;
    -webkit-text-fill-color: #d2d2d2;
  }
  .center{
    padding-left: .875rem;
    width: 100%;
    border-top: 1px solid #ededed;
    height:2.8125rem ; 
    line-height: 2.8125rem ;
    position: relative;
    border-bottom: 1px solid #ededed;
  }
  .center span{
    display: inline-block;
    width: 100%;
    padding-right: 1.6875rem;
  }
  .dayu{
    display: inline-block;
    position: absolute;
    top:34%;
    right: 2%;
    background: url(../../assets/icon/dayu.png) no-repeat ;
    width:14px;
    height:15px;
    background-size:100%; 
    opacity: .3;
    margin: auto 0;
  }
  .bottom{
    width: 100%;
    height:4.06rem ;
    padding: .6875rem  .6875rem  .6875rem .875rem;
    font-size:.94rem;
    word-wrap: break-word;
    border-bottom: 1px solid #ededed;
    position: relative;
  }
  .bottom textarea{
     height: 2.75rem;
     width: 83%;
     outline: 0;
     border: 0;
     -webkit-text-fill-color: #d2d2d2;
     font-size: 1.2rem;
  }
  .position-ico{
    position: absolute;
    right: .94rem;
    top:.94rem;
    width: 1.5rem;
    height: 2.125rem;
    background: url(../../assets/icon/position.png) no-repeat;
    background-size: contain;
  }
  .btn{
    width: 18.125rem;
    height:2.69rem;
    line-height: 2.69rem;
    font-size: 1.1rem;
    color: #fff;
    border-radius: 5px;
    margin: .94rem auto;
    background: #e02e24;
    text-align: center;
    opacity: .2;
  }
  .content{
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    display:none;
  }
  .addAddress >>> .hi{
    float: right;
    margin: .625rem 1rem 0;
  } 
  .content .bg{
    width: 100%;
    height: 100%;
    position: absolute;
    background: rgba(0,0,0,.8)
  }
  .distpicker-address-wrapper{
    width: 100%;
    height: 24.125rem;
    background: #fff;
    position: absolute;
    bottom: 0;
    overflow: hidden;
    transform:translateY(25rem);
    transition:all 0.5s;
    color: #151516
  }
  .addAddress >>> .distpicker-address-wrapper .address-container{
    width: 100%;
    height: 21.25rem;
  }
  .addAddress >>> .distpicker-address-wrapper .address-container ul{
    overflow: scroll
  }
  .addAddress >>> .distpicker-address-wrapper .address-container ul::-webkit-scrollbar {
    display: none;
  }
  </style>
  <style>
  .distpicker-address-wrapper .address-header ul {
    justify-content: start;
  }
  .distpicker-address-wrapper .address-header ul  li{
    margin:0 .625rem ;
    padding:10px  0;
  }
  </style>
