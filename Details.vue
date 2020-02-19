<template >
  <div class="main" @scroll="scroll" v-if="listC.img1">
    <div class="container">
      <div class="no_scroll">      
        <div class="bar">
          <div class="bar-item" @click="prev">
            <span></span>
          </div>
          <div class="bar-item">
            <span></span>
          </div>
        </div>
      </div> 
      <div class="scroll-bar">
        <div class="back" @click="prev"><span></span></div>
        <nav class="scroll_title">
          <a @click="jump('.main',0)" :class="{clickBG:0==current}">商品</a>
          <a @click="jump('.details',1)" :class="{clickBG:1==current}">详情</a>
        </nav>
        <div class="more"><span></span></div>
      </div>
      <mt-swipe >
        <mt-swipe-item >
          <img :src="'http://127.0.0.1:4000/'+listC.img1" alt="">
        </mt-swipe-item>
        <mt-swipe-item >
          <img :src="'http://127.0.0.1:4000/'+listC.img2" alt="">
        </mt-swipe-item>
        <mt-swipe-item >
          <img :src="'http://127.0.0.1:4000/'+listC.img3" alt="">
        </mt-swipe-item>
          <mt-swipe-item >
          <img :src="'http://127.0.0.1:4000/'+listC.img4" alt="">
        </mt-swipe-item>
      </mt-swipe>
      <div class="banner">
        <img src="../../assets/details/20191214143950.png" alt="">
        <!-- <div class="promotion-countdown-wrap">
            <span>返场倒计时</span>
            <div>
              <div class="time"><span class="my-hour">{{hour}}</span></div>
              <span>:</span>
              <div class="time"><span class="my-minute">{{minute}}</span></div> 
              <span>:</span>
              <div class="time"><span class="my-second" >{{second}}</span></div> 
            </div>
        </div> -->
      </div>
      <div class="price-item">
        <span class="spans font-center" >
          <span>¥</span>
          <span>{{list.price}}
            <span>起</span>
          </span>  
        </span>   
        <span>
          <del>
            ¥{{list.price2}}     
          </del>
        </span>
        <span>已拼{{total}}万件</span>
      </div>
      <div class="title">
        <img src="../../assets/icon/e01ec845d67c3717fd0581da8dbf86bd.png" alt="">
          <span>{{list.title}}</span>         
      </div>
      <div class="quan">
        <div class="quanl"> 
          <div style="display:flex">
          <div class="quan-v1">领劵</div>
          <div class="quan-v2">满33元减2元</div>
          <div class="quan-v3">满33元减2元</div>   
          </div>    
          <span class="dayu"></span>
          </div>
      </div>
      <div class="promise">
        <div class="promise-v1">
          <div>{{list.promise}}</div>
        </div>
        <span class="dayu"></span>
      </div>
      <div class="mycarousel">
        <mt-swipe>
          <mt-swipe-item v-for="(item,i) of user" :key="i"> 
              <div class="carousel">
              <span class="avatar" :style="{backgroundImage: 'url('+ require('../../assets/portrait/1.jpg') +')'}"></span>
              <div class="center">
              <span class="nickname">用户{{item.uid}}</span>
              <div>
              <p>还差<span>1人</span>拼成</p >
              <p class="time1">剩余{{hour[i]}}:{{minute[i]}}:{{second[i]}}</p>
              </div>
              </div>
              <div class="go" @click="go" :data-uid="item.uid" :data-h="hour[i]" :data-m="minute[i]" :data-s="second[i]" >去拼单</div> 
            </div>
          </mt-swipe-item>
          <mt-swipe-item>
            <div class="carousel">
              <span class="avatar al" :style="{backgroundImage: 'url('+ require('../../assets/portrait/1.jpg') +')'}"></span>
              <span class="avatar ar" :style="{backgroundImage: 'url('+ require('../../assets/portrait/2.jpg') +')'}"></span>
              <div class="center">
              <span class="nickname">周润发、刘亦菲</span>
              </div>
              <div class="go" >拼单成功</div>
            </div>
          </mt-swipe-item>
        </mt-swipe>
      </div>
      <div class="details">
        <p>商品详情</p>
        <div class="details-attr">
          <div class="attr-item">
            <span class="key">产地</span>
            <span class="value">{{list.field}}</span>
          </div>
          <div class="attr-item">
            <span class="key">包装方式</span>
            <span class="value">{{list.manner}}</span>
          </div>
          <div class="attr-item">
            <span class="key">净含量</span>
            <span class="value">{{list.content}}</span>
          </div>
          <div class="attr-item">
            <span class="key">保存状态</span>
            <span class="value">{{list.state}}</span>
          </div>
        </div>
        <div class="imgs">
          <img :src="'http://127.0.0.1:4000/'+listC.img_details1">
          <img :src="'http://127.0.0.1:4000/'+listC.img_details2">
          <img :src="'http://127.0.0.1:4000/'+listC.img_details3">
          <img :src="'http://127.0.0.1:4000/'+listC.img_details4">
          <img :src="'http://127.0.0.1:4000/'+listC.img_details5">
          <img :src="'http://127.0.0.1:4000/'+listC.img_details6">
        </div>
      </div>
      <div class="bottom">
        <div class="gn">
          <i class="more"></i>
          <span>更多</span>
        </div>
        <div class="gn">
          <i class="collection"></i>
          <span>收藏</span>
        </div>
        <div class="gn">
          <i class="service"></i>
          <span>客服</span>
        </div>
        <div class="buy" @click="pay(listP.only)">
          <span>¥{{listP.only}}</span>
          <span>单独购买</span>
        </div>
        <div class="buy share" @click="pay(listP.price)">
          <span>¥{{listP.price}}</span>
          <span>发起拼单</span>
        </div>
      </div>
      <div class="goC"> 
        <div class="bg"></div>
        <div class="join">
          <p class="name">参加<span>用户{{uid}}</span>的拼单</p >
          <p class="msg">仅剩<span class="num">1</span>个名额，<span>{{h}}:{{m}}:{{s}}</span>后结束</p >
          <div class="cancel" @click="cancel"></div>
          <ul>
          <li class="avatar" :style="{backgroundImage: 'url('+ require('../../assets/portrait/1.jpg') +')'}">
          <span class="host">拼主</span>
          </li>
          <li class="unjoin"></li>
          </ul>
          <div class="btn" @click="pay('group')">参与拼单</div>
        </div>
      </div>
    </div>
   </div>
</template>

<style scoped>
  body{
    color: #666;
    font-size: 12px;
    line-height: 1.5;
  }
  div{
    background: #fff 
  }
  .value{
    width:12rem;
    display: inline-block;
    vertical-align: top;
  }
  .container{
    height: 335px;
  }
  .bar{
    width: 100%;
    min-height:44px;
    position: fixed; 
    display: flex;
    justify-content: space-between;
    z-index: 101;
    background: transparent
  }
  .bar>.bar-item{
    width: 30px;
    height: 30px;
    padding: 5px;
    background: #666;
    border-radius:20px;
    margin: 7px 0 0 5px;
  }
  .bar>div:last-child{
    margin-right:5px
  }
  .bar-item>span{
    width: 20px;
    height: 20px;
    display: inline-block;
    background:url(../../assets/jiantou.png) no-repeat 50%;
    background-size:20px 20px; 
  }
  div.bar-item:last-child>span{
    background-image:url(../../assets/diandian.png)
  }
  .container >>> .mint-swipe-indicator{
    width: 7px;
    height: 7px;
    opacity: 0.8;
    background: #666; 
  }
  .container >>>  .mint-swipe-indicators{
      left: 80%;
  }
  .container >>> .mint-swipe-indicator.is-active{
    background: #c23531;
  }
  .container img{
    width: 100%;
    height: 100%;
  }
  .banner{
    position: relative;
  }
  .promotion-countdown-wrap{
    height: 100%;
    width: 30%;
    display: flex;
    position: absolute;
    text-align: center;   
    right: 0;
    top:0;
    color:#fff;
    padding: .2rem 0; 
    align-items:center; 
    flex-wrap: wrap;
    background: transparent;
  }
  .promotion-countdown-wrap>span{
      width: 100%;
      font-size: .8rem;
  }
  .promotion-countdown-wrap>div{
    width: 100%;
    display: flex;
    justify-content: center;
    font-size: .12rem;
    height: 18px;
    background: transparent
  }
  .promotion-countdown-wrap>div>span{
      font-size:1rem ;
  }
  .time{
    background: #a60004;
    width: 15%;
    border-radius: .02rem;
    text-align: center;
    height: 100%;
    
  }
  .time>span{
    display: inline-block;
    height: 100%;
    line-height: 1.5;
  }
  .price-item{
    height: 2.3rem;
    overflow: hidden;
    color:#e02E24;
    box-sizing: content-box;
    padding: 0.4rem .75rem  0 .625rem;
    display: flex;
    justify-content: flex-start;
    align-items: center;
    flex-direction: row;
    
  }
  .spans{
    height:28px;
    line-height: 28px;
    font-weight: 700;
  }
  .font-center{
    font-family:     PingFangSC-Regular,STHeiti STXihei,Microsoft YaHei,Microsoft JhengHei
  }
  .spans>span:first-child{
    font-size:15px;
    margin: 0 2px;
  }
  .spans>span:nth-child(2){
    font-size: 28px;
  }
  .spans>span:nth-child(2)>span{
    font-size: 12px;
    line-height: 16px;
    position: relative;
    left:2px;
    bottom:1px;
    font-weight: 400;
  }
  .price-item>span:nth-child(2){
    height: 100%;
    line-height: 35px;
    margin-left:6px;
    position: relative; 
    top:5px;
    color:#58595b;
    font-size:13px;
  }
  .price-item>span:last-child{
    flex: 1;
    color: #58595b;
    font-size:13px;
    text-align: right
  }
  .title{
    position: relative;
    width: 100%;
    font-size: 0.95rem;
    line-height: 1.4;
    color:#151516;
    overflow: hidden;
    font-weight: 700;
    padding:  .375rem .25rem 0 .625rem;
  }
  .title>img{
    width:2.5rem;
    height:1.05rem ;
    display: inline-block;
    max-width: 100%;
    position: relative;
    top:0.125rem;
    margin-right:0.4rem 
  }
  .quan{
    padding:.5rem 0;
    margin-bottom: 1px;
    border-bottom:1px solid #f2f2f2;
    margin-top:-8px; 
  }
  .quanl,.promise{
    display: flex;
    justify-content: space-between;
    padding: 0.5rem
  }
  .quan-v1,.quan-v2,.quan-v3{
    border-radius: 2px;
    border: 1px solid #e02e24;
    text-align: center;
    height: 1.125rem;
    line-height: 1.125rem;
    font-size: 0.67rem;
  }
  .quan-v1{
    justify-content: center;
    width:2rem;  
    background: #e02E24;
    color:#fff; 
  }
  .quan-v2,.quan-v3{
    padding: 0 5px;
    color:#e02E24;  
  }
  .quan-v2{
    margin-left: 0.5rem; 
  }
  .quan-v3{
    margin-left: .25rem;
  }
  .dayu{
    display: inline-block;
    background: url(../../assets/icon/dayu.png) no-repeat ;
    width:14px;
    height:15px;
    background-size:100%; 
    opacity: .3;
    margin: auto 0;
  }
  .promise{
    color: #58595b;
    font-size:0.8125rem 
  }
  .mycarousel{
    width: 100%;
    margin-top: 0.5rem;
    height: 55px;
  }
  .carousel{
    background: #fff;
    display: flex;
    justify-content: space-between;
    padding: 0.5rem .75rem 0;
    height: 55px;
    width: 100%
  }
  .carousel .avatar{
    background-size: 100%;
    width: 2.3rem;
    height: 2.3rem;
    display: inline-block;
    background-repeat: no-repeat;
    border-radius: 50%;
  }
  .carousel .avatar.al{
    margin-right: -1.37rem;
  }
  .carousel .avatar.ar{
    margin-right: .5rem;
  }
  .center{
    width: 14.5rem;
    display: flex;
    justify-content:space-between
    }
  .carousel .nickname{
    display: inline-block;
    line-height: 2rem;
    }
  .center>div{
    line-height: 1rem;
    }
  .center p{
    font-size: .8rem;
    color: #151516;
    }
  .center p.time1{
    color: #58595b
    }
  .center p span{
    color: #e02e24
    }
  .carousel .go{
    width: 4.25rem;
    height: 1.9rem;
    line-height: 1.9rem;
    text-align: center;
    background: #e02e24;
    color: #fff;
    border-radius: .25rem
  }
  .container>>>.mint-swipe-indicator{
    width:0px;
  }
  .details{
    margin-top: 0.5rem;
    padding: 0 .75rem;
  }
  .details>p{
    height: 2.5rem;
    line-height: 2.5rem;
    font-size: 1rem
  }
  .details-attr{
    background: #f3f3f3;
    padding: 0.5rem 0.8rem;
    margin-bottom: .7rem;
  }
  .details-attr .attr-item{
    background: transparent;
    font-size: .875rem;
    padding: 0.25rem 0;
  }
  .details-attr .attr-item .key{
    color: #9c9c9c;
    display: inline-block;
    width: 7rem;
  }
  .bottom{
    width: 100%;
    height: 3.4rem;
    position: fixed;
    z-index: 10001;
    bottom: 0;
    display: flex;
  }
  .gn{
    padding: 0.5rem 0;
    margin: 0 .53rem;
  }
  .bottom i{
    background: url(../../assets/more.png) no-repeat;
    background-size: 100%;
    display: block;
    width: 1.5rem;
    height: 1.5rem;
  }
  .bottom i.collection{
    background: url(../../assets/collection.png) no-repeat;
    background-size: 100%;
  }
  .bottom i.service{
    background: url(../../assets/service.png) no-repeat;
    background-size: 100%;
  }
  .gn span{
    font-size: .75rem;
    color: #555;
  }
  .buy{
    width: 7.5rem;
    background: #f3aba7;
    text-align: center;
  }
  .buy.share{
    background: #e02e24;
  }
  .buy span{
    display: block;
    margin: 0.4rem 0;
    color: #fff
  }
  .goC{
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    background: transparent; 
    z-index: 201;
    display: none;
  }
  .goC .bg{
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, .8);
    position: fixed;
    left: 0;
    top: 0;
  }
  .goC .join{
    width: 18.12rem;
    height: 14.125rem;
    z-index: 202;
    position: fixed;
    left: 0;
    top: 0;
    margin: auto;
    bottom: 4rem;
    right: 0;
    padding: 1.81rem 1.25rem;
  }
  .goC .join p{
    text-align: center;
    font-size: 1.06rem;
  }
  .goC .join .name span{
    display: inline-block;
    max-width: 6.25rem;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    vertical-align: bottom;
  }
  .goC .join .msg{
    color: #58595b;
    font-size: .875rem;
    margin-top: 0.5rem;
  }
  .goC .join .msg .num{
    color: #e02e24;
  }
  .goC .join ul{
    height: 3.12em;
    margin: 0 auto;
    padding: 1rem 0;
    box-sizing: content-box;
    display: flex;
    justify-content: center
  }
  .goC .join li{
    width: 3rem;
    height: 3rem;
    background-size: 100%;
    background-repeat: no-repeat;
    border-radius: 50%;
    position: relative;
  }
  .goC .join li.unjoin{
    background: url(../../assets/unjoinA.png) no-repeat;
    border: 1px dashed #ccc;
    background-size: .68rem 1rem;
    background-position: 50%;
    margin-left: 0.375rem;
  }
  .goC .join .host{
    width: 2.37rem;
    height: 1rem;
    line-height: 1rem;
    display: block;
    background: #ffab33;
    border: 1px solid #fff;
    border-radius: .75rem;
    font-size: .68rem;
    text-align: center;
    color: #9f7200;
    position: absolute;
    top: -0.32rem;
    left: -0.2rem;
  }
  .goC .join .btn{
    font-size: 1.06rem;
    color: #fff;
    background: #e02e24;
    text-align: center;
    padding: 0.56em;
  }
  .goC .cancel{
    background: url(../../assets/orders/cancel.png) no-repeat;
    background-size: 100%;
    width: 1.82rem;
    height: 1.82rem;
    position: absolute;
    right: -.8rem;
    top: -.9rem;
  }
  .scroll-bar{
    width: 100%;
    display: flex;
    justify-content: space-around;
    min-height: 2.75rem;
    border-bottom: 1px solid #e5e5e5;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 300;
    opacity: 0;
  }
  .scroll-bar>div{
    width: 2.5rem;
    height: 2.75rem;
    line-height: 3.4rem;
    text-align: center;
    background: transparent
  }
  .scroll-bar>div>span{
    background: url(../../assets/details_back.png) no-repeat;
    background-size: 100%;
    display: inline-block;
    width: 1.25rem;
    height: 1.25rem;
  }
  .scroll-bar>div.more>span{
    background: url(../../assets/details_more.png) no-repeat;
    background-size: 100%;
    background-position: center
  }
  .scroll_title{
    width: 235px;
    line-height: 2.75rem;
    display: flex;
    justify-content: space-around
  }
  .scroll-bar a{
    font-size: .875rem
  }
  .clickBG{
    background: url(../../assets/position.png) no-repeat;
    background-size: .85rem;
    background-position-y: center;
    padding-left: 1.1rem;
    color: #249f1d;
  }
</style>
<script>
export default {
  data(){
    return{
      list:[],//产品嘻嘻
      listP:[],//图片路径
      listC:[], //产品价格
      user:[],
      hour:[],
      minute:[],
      second:[],//
      total:5.8,
      pid:"",
      order_time:"",
      uname:"",
      times:[],
      c:"",
      uid:"",//用户id
      h:"", //点击拼单剩余小时
      m:"",//点拼单剩余分
      s:"",//点拼单剩余秒
      current:0,
      newuid:""
    }
  },
  beforeMount() {
    this.load();
    this.img();
    this.order();
  },
  mounted(){
    window.addEventListener("scroll",this.scroll)
  },
  beforeDestroy(){
    window.removeEventListener("scroll",this.scroll)
  },
  methods:{
    // 拼单用户信息
    order(){
      var day=86400000;  //24小时
      var url="findcart";
      // console.log(this.pid);
      var obj={share_state:1,pid:this.pid};
      this.axios.get(url,{params:obj}).then(res=>{   
        this.user=res.data.data;
        // 倒计时
        // console.log(this.pid)
        if(res.data.code==1){
        for(var i=0;i<this.user.length;i++){   
          var current=new Date().getTime();
          var remaining= (day-(current -this.user[i].order_time));//剩余时间
         // console.log(remaining)
          var horus=parseInt(remaining%(1000*60*60*24)/(1000 * 60 * 60));//获取小时         
          var minutes = parseInt((remaining % (1000 * 60 * 60)) / (1000 * 60));//获取分   
          var seconds =parseInt((remaining % (1000 * 60)) / 1000);                
            if(horus<=0&&minutes<=0&&seconds<=0){
                var url="upatecart";                
                var obj={share_state:4,pid:this.pid,uid:res.data.data[i].uid};//uid当前用户
                this.axios.get(url,{params:obj}).then(res=>{
                })
            }else{
                 this.hour.push(horus);//添加到数组里
                this.minute.push(minutes);
                 this.second.push(seconds);
            }
          } //for结尾
        } //if结尾          
      })
    },
    time(){
      
    },
    img(){
      var url="pic";
      var obj={pid:this.pid};
      this.axios.get(url,{params:obj}).then(res=>{
        this.listC=res.data.data[0];
        //  console.log(this.listC)
     })
    },
    load(){
      var url="details";
      var str=window.location.href;//获取地址栏rul
      this.pid=str.split("=")[1];//pid的值
      var obj={pid:this.pid};
      this.axios.get(url,{params:obj}).then(res=>{     
         this.list=res.data.data[0];
      });
      url="price";  
      this.axios.get(url,{params:obj}).then(res=>{
        this.listP=res.data.data[0];    
      });
    },
    time(){  
      //  setInterval(()=>{
      //    if(j<=0){
      //      j=59;
      //    }else{
      //     --j;
      //    }
      //  console.log(j)
      //  },1000);
      //   return j;
      //    var s= setInterval(()=>{
      //       if(this.second<=0){              
      //          this.second[i]=59;          
      //         }  
      //        else{
      //         --this.second[i];
      //     }
      //       if(this.minute==0&&this.hour==0&&this.second==0){
      //           clearInterval(s);
      //           clearInterval(m);
      //           clearInterval(h);
      //           //移除该元素
      //       }
      //     }, 1000);
      //       var m= setInterval(()=>{
      //     if(this.minute[i]<=0){
      //        this.minute[i]=59
      //     }else{
        
      //   }
      // }, 60000);
      // var h= setInterval(()=>{
      //   if(this.minute<=0){
      //     this.minute=0
      //   }else{
      //     --this.minute;
      //    }
      //   }, 360000);   
    },
    prev(){
      this.$router.go(-1)
    },
    async  pay(p){
      if(p=='group'){
        p=this.list.price;
     let res=  await this.axios.get("/login")
        this.newuid=res.data.data;
      
      }else{
         let res=  await this.axios.get("/login")
         this.uid=res.data.data;
      }

      this.$router.push({name:"Pay",query:{
          newuid:this.newuid,
          uid:this.uid,
          pid:this.pid,
          price:p,
          pic:this.listC.img1,
          way:p==this.list.only?"o":"t",
          title:this.list.title
        }})
       
      // if(p=='group'){  
      // p=this.list.price
      // this.axios.get("/login").then(res=>{
      //   console.log(res.data.data)
      //   this.newuid=res.data.data;
      //    this.$router.push(`/Pay?uid=${this.uid}&newuid=${this.newuid}&pid=${this.pid}&price=${p}&pic=${this.listC.img1}&${p==this.list.only?"o":"t"}`)
      // }) }else{
      // this.$router.push(`/Pay?pid=${this.pid}&price=${p}&pic=${this.listC.img1}&${p==this.list.only?"o":"t"}`)
      // }     
   
    },
    go(e){
      this.uid=e.target.dataset.uid;
      this.h=e.target.dataset.h;
      this.m=e.target.dataset.m;
      this.s=e.target.dataset.s;
      document.querySelector(".goC").style.display="block"
    },
    cancel(){
      document.querySelector(".goC").style.display="none"
    },
    scroll(){
      var scrollT=document.querySelectorAll(".scroll_title")[0]
      if(window.scrollY==100){
        document.querySelector(".scroll-bar").style.opacity=".5";
        document.querySelector(".no_scroll").style.display="none"
      }else if(window.scrollY>100){
        document.querySelector(".scroll-bar").style.opacity="1"
      }else if(window.screenY==0){
        document.querySelector(".scroll-bar").style.opacity="0";
        document.querySelector(".no_scroll").style.display="block"
        document.querySelector(".no_scroll").style.zIndex=500
     }
     if(window.scrollY>582){
        scrollT.lastChild.classList.add("clickBG")       
        scrollT.firstChild.classList.remove("clickBG")       
      }else{
        scrollT.lastChild.classList.remove("clickBG")       
        scrollT.firstChild.classList.add("clickBG") 
      }
    },
    jump(j,i){
      var leng= document.querySelector(j).offsetTop; 
      this.current=i;
     
      $("body,html").animate({
        scrollTop:0+leng
      },1000)
    }
  }
}
</script>

