<template>
  <div class="mine">
    <div class="head">
      <div class="avatar">
        <img src="../../assets/avatar.png">
      </div>
      <span class="nickname" @click="login" ref="phone">{{yes}}</span>
    </div>
    <div class="main">
      <div class="order">
        <div class="title">
          <h4>我的订单</h4>
          <span @click="order">查看全部订单<i class="skip"></i></span>
        </div>
        <div class="menu">
          <div class="menu-item">
            <div class="img unpayed"></div>
            <span>待付款</span>
          </div>
          <div class="menu-item">
            <div class="img shipping"></div>
            <span>待收货</span>
          </div>
          <div class="menu-item">
            <div class="img unrated"></div>
            <span>待评价</span>
          </div>
          <div class="menu-item">
            <div class="img after-sales"></div>
            <span>退款/售后</span>
          </div>
        </div>
      </div>
      <div class="tool">
        <div class="title">
          <h4>常用功能</h4>
        </div>
        <div class="menu">
          <div class="menu-item">
            <div class="img ticket"></div>
            <span>领券中心</span>
          </div>
          <div class="menu-item">
            <div class="img address"></div>
            <span>收货地址</span>
          </div>
          <div class="menu-item">
            <div class="img gift"></div>
            <span>邀请有礼</span>
          </div>
          <div class="menu-item">
            <div class="img collect"></div>
            <span>商品收藏</span>
          </div>
          <div class="menu-item">
            <div class="img evaluate"></div>
            <span>我的评价</span>
          </div>
          <div class="menu-item">
            <div class="img service"></div>
            <span>联系客服</span>
          </div>
          <div class="menu-item">
            <div class="img opinion"></div>
            <span>意见反馈</span>
          </div>
          <div class="menu-item">
            <div class="img set"></div>
            <span>设置</span>
          </div>
        </div>
      </div>
    </div>
    <recommend></recommend>
    <foot :j="j"></foot>
  </div>
</template>
<script>
import Recommend from './Recommend.vue'
import Foot from './Foot.vue'
export default {
  data(){
    return{
      j:3,
      yes:"立即登录"
    }
  },
  components:{
    Recommend,
    Foot
  },
  created(){
    this.showP()
  },
  methods:{
    login(){
      this.$router.push("/LoginReg")
    },
    order(){
      this.$router.push("/Orders")
    },
    showP(){
      var url="verify";
      this.axios.get(url).then(res=>{
        if(res.data.code==1){
        // this.yes=res.data.data[0].phone
        var reg = /^(\d{3})\d{4}(\d{4})$/;
        this.yes=res.data.data[0].phone.replace(reg,"$1****$2");
        this.$refs.phone.style.color="#FF9800"
        }
      })
    }
  }
}
</script>
<style scoped>
  .head{
    display: flex;
    padding: 0.5rem 0.7rem;
  }
  .avatar{
    width: 2.6rem;
    height: 2.6em;
  }
  .avatar img{
    width: 100%;
    height: 100%;
    border-radius: 50%
  }
  .nickname{
    margin: auto .6rem;
    color: #999;
  }
  .main{
    padding: 0 0.75rem;
  }
  .main>div{
    background: #fff;
    padding: 1rem .7rem 0;
  }
  .order{
    margin: 0.6rem 0;
  }
  .order .title{
    display: flex;
    justify-content: space-between
  }
  .order .title span{
    color: #999;
    font-size: .75rem;
  }
  .order .title i{
    background: url(../../assets/skip.png) no-repeat;
    background-size: 100%;
    display: inline-block;
    width: 12px;
    height: 12px;
    opacity: .5;
    position: relative;
    top: 0.07rem;
    left: 0.2rem;
  }
  .menu{
    display: flex;
    justify-content: space-around;
    padding: 1rem 0 ;
    width: 100%;
  }
  .menu-item{
    width: 25%;
    text-align: center
  }
  .menu .img{
    background: url(../../assets/unpayed.png) no-repeat;
    background-size: 100%;
    width: 1.7rem;
    height: 1.7rem;
    display: block;
    margin: 0 auto .4rem;
  }
  .menu .img.shipping{
    background: url(../../assets/shipping.png) no-repeat;
    background-size: 100%;
  }
  .menu .img.unrated{
    background: url(../../assets/unrated.png) no-repeat;
    background-size: 100%;
  }
  .menu .img.after-sales{
    background: url(../../assets/after-sales.png) no-repeat;
    background-size: 100%;
  }
  .menu .img.ticket{
    background: url(../../assets/quan.png) no-repeat;
    background-size: 100%;
  }
  .menu .img.address{
    background: url(../../assets/shouhuodizhi.png) no-repeat;
    background-size: 100%;
  }
  .menu .img.git{
    background: url(../../assets/li.png) no-repeat;
    background-size: 100%;
  }
  .menu .img.collect{
    background: url(../../assets/shoucang.png) no-repeat;
    background-size: 100%;
  }
  .menu .img.evaluate{
    background: url(../../assets/pingjia.png) no-repeat;
    background-size: 100%;
  }
  .menu .img.service{
    background: url(../../assets/lianxikefu.png) no-repeat;
    background-size: 100%;
  }
  .menu .img.opinion{
    background: url(../../assets/yijian.png) no-repeat;
    background-size: 100%;
  }
  .menu .img.set{
    background: url(../../assets/shezhi.png) no-repeat;
    background-size: 100%;
  }
  .menu span{
    font-size: .7rem;
    color: #666;
    text-align: center;
  }
  .tool .menu{
    flex-flow: wrap;
    padding: 1rem 0 0;
  }
  .tool .menu-item{
    margin-bottom: 1.6rem;
  }
</style>
