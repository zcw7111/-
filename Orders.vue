<template>
  <div class="orders">
    <div class='search'>
      <i class="mintui mintui-back" @click="back"></i>
      <div >
          <i class="mintui mintui-search"></i>
          <input type="text" placeholder="请输入商品名称">
      </div>          
      <span>搜索</span>
    </div>
    <ul class="bar">
      <li @click="change(0)" :class="{listItem:0==current}">全部</li>
      <li @click="change(1)" :class="{listItem:1==current}">待付款</li>
      <li @click="change(2)" :class="{listItem:2==current}">待分享</li>
      <li @click="change(3)" :class="{listItem:3==current}">待收货</li>
      <li @click="change(4)" :class="{listItem:4==current}">待评价</li>
    </ul>
    <div class="line"></div>
    <div class="main">
      <div class="content" v-if="show==0">
        <div class="details">
          <p>待收货</p>
          <div>
            <img src="../../assets/imgs/3d908cf741a417a3e4e11c4cf3d770c1.jpeg" alt="">
            <div class="title">
              <p>棉拖鞋女冬季情侣防滑保暖家居家用厚底室内月子包跟毛毛拖鞋男士</p>
              <p>格子款 青灰色,【42/43码】【适合41-42脚】</p>
            </div>
            <div>
              <div class="price">
                <span>¥</span>
                1
              </div>
              <div class="count">
                ×1
              </div>
            </div>
          </div>
        </div>
        <div class="center">
          <div class="portrait">
            <img src="../../assets/portrait/1.jpg" alt="">
            <img src="../../assets/portrait/1.jpg" alt="">
            <img src="../../assets/portrait/1.jpg" alt="">
          </div>
          <div class="prc">
            <span>实付:</span>
            <span>¥7.2</span>
            <span>(免运费)</span>
          </div>
        </div>
        <div class="btn">
            <a>申请退款</a>
            <a>延长收货</a>
            <a>查看物流</a>
            <a>确认收货</a>
        </div>
        <div class="bottom">您已经没有更多的订单了</div>
      </div>
      <!-- <div class="content" v-else-if="show==1">
        <div>
          <p>您还没有相关的订单</p>
        </div>
      </div>
      <div class="content" v-else-if="show==2">
        <div>
          <p>待分享</p>
        </div>
      </div>
      <div class="content" v-else-if="show==3">
        <div>
          <p>待收货</p>
        </div>
      </div>
      <div class="content" v-else-if="show==4">
        <div>
          <p>待评价</p>
        </div>
      </div> -->
    </div>
  </div>
</template>
<script>
export default {
  data(){
    return{
      current:0,
      show:0
    }
  },
  beforeCreate(){
    $("body")[0].style.background="#f5f5f5"
  },
  beforeDestroy() {
    $("body")[0].backgroundImage="-webkit-linear-gradient(top,#f3fbcc,#afe471)"
  },
  methods:{
    change(i){
      this.current=i;
      this.show=i
    },
    back(){
      this.$router.go(-1)
    }
  }
}
</script>
<style  scoped>
  .orders{
    color: #151516;
  }
  .search{
    display: flex;
    justify-content: space-between;
    background: #91c7ae;
    padding: .3rem .6rem;
    align-items: center;
    height:2.875rem ;
    color: #fff;
    margin-bottom: 0.5rem;
  }
  .mintui.mintui-back{
    font-size:1.5rem;
    font-weight:550;
  }
  .search>div{
    width: 75%;
    position: relative;
    height: 77%;    
  }
  .mintui.mintui-search{
    position: absolute;
    font-size: 1rem;
    color:#d9d9d9;
    top:25%;
    left:5%;
  }
  .search input{
    height: 100%;
    padding-left:2.2rem; 
    width: 100%;
    -webkit-text-fill-color: #d9d9d9;
    outline: 0;
    border: 0;
    border-radius: 20px;
    font-size:1rem ;
  }
  .search span{
    font-size:0.88rem;
    margin-right:0.3rem; 
  }
  .line{
    height: 1px;
    background: #ddd;
  }
  .bar{
    display: flex;
    justify-content: space-around;
    height: 2.5rem;
  }
  .listItem{
    color:#92d65d;
    border-bottom:1px solid #92d65d; 
  }
  .bar>li{
    line-height: 2.5rem;
    font-size: .9rem;
  }
  .details{
    background: #fff;
    font-size: 0.75rem;
  }
  .details>p{
    height: 2.5rem;
    color: #92d65d;
    padding: 0 .625rem;
    text-align: right;
    font-size: 0.8125rem;
    line-height: 2.5rem;
  }
  .details>div{
    display: flex;
    justify-content: space-between;
    padding: .375rem .625rem;
    background: #f5f5f5;
  }
  .details>div>img{
    width: 22%;
    margin-right:.75rem;
    border-radius:2px;  
  }
  .title{
     width:63%;
     margin-right:1.125rem;
     overflow: hidden; 
     font-size:0.8125rem;
   }
   .title>p:first-child{
     text-overflow: ellipsis;
     display:box;
     line-clamp: 2;
     box-orient: vertical;
     line-height: 1.18rem;
     max-height: 3.56rem;
   }
   .title>p:last-child{
     margin-top:.187rem;
     color:#9c9c9c;
     font-size: .75rem;
     white-space: pre-line;
     line-height: 1rem
   }
   .details>div>div:last-child{
     text-align: right;
     line-height: 1.1875rem;  
   }
   .price{
     font-size: .875rem;
   }
   .count{
     font-size: .75rem;
     color:#9c9c9c
   }
   .center{
     margin-right: .625rem;
     display:flex;
     justify-content: space-between; 
     align-items: center;
      background: #fff;
   }
   .portrait{
     padding: .44rem 0 .44rem .625rem;
    
   }
   .portrait>img{
     width: 1.625rem;
     height: 1.625rem;
     border-radius: 50%;
     margin-left:-.5rem; 
   }
   .portrait>img:first-child{
     margin-left: 0;
   }
   .prc span{
      font-size:.75rem;
      margin-right: .125rem;
   }
   .prc span:nth-child(2){
     font-size: 1rem
   }
   .prc span:last-child{
     margin-right: 0;
   }
   .btn{
     font-size: .875rem;
     display: flex;
     justify-content: flex-end;
     padding-top: .44rem;
     margin-right:.625rem ;
     background: #fff;
   }
   .btn>a{
     height: 1.875rem;
     min-width: 4.69rem;
     margin-right: .375rem;
     border:1px solid #9c9c9c; 
     border-radius: .25rem;
     line-height: 1.875rem;
     text-align: center;
   }
  .btn>a:active{
    background:#ddd;
   }
   .btn>a:last-child{
     background: #92d65d;
     color:#fff;
     border: 0;
     margin-right:0 
   }
  .bottom{
    height:2.8rem ;
    text-align: center;
    line-height: 2.8rem;
    color:#9c9c9c;
    font-size: .875rem;
    margin-bottom:.625rem 
  }
</style>