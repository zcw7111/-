<template>
  <div class="order">
    <div class="top">
      <i class="mintui mintui-back" @click="back"></i>
      确认订单
    </div>
    <div class="address" @click="addAddress" v-if="address.length==0">
      <i class="add"></i>
      <span ref="dizhi">手动添加收货地址</span>
      <i class="skip"></i>
    </div>
    <div class="show_add" v-else @click="addAddress">
      <i class="position"></i>
      <div class="information">
        <div class="roof">
          <span class="name">{{this.address[0].receiver}}</span>
          <span class="phone">{{this.address[0].cellphone}}</span>
        </div>
        <div class="bot">{{this.address[0].address}}</div>
      </div>
      <i class="more"></i>
    </div>
    <my-address v-if="add" @func="get" :uid=uid></my-address>
    <div class="line"></div>
    <div class="product">
      <img class="img" :src="lco+pic">
      <div class="details">
        <p class="title">{{title}}</p>
        <p class="price">¥{{price}}/件</p>
      </div>
    </div>
    <div class="num">
      <span>购买数量</span>
      <div>
        <button @click="num(-1)" class="sub" >－</button>
        <input type="text" v-model="n">
        <button @click="num(+1)">＋</button>
      </div>
    </div>
    <div class="bottom">
      <span>平台用户信息安全由</span>
      <div></div>
      <span>承保</span>
    </div>
    <div class="pay">
      <p>
        实付款：
        <span class="price">¥{{total}}</span>
        <span>免运费</span>
      </p>
      <div class="btn" @click="pay">立即支付</div>
    </div>
  </div>
</template>
<script>
import Address from "./Address.vue"
export default {
  data(){
    return{
      list:[],
      price:"",
      pid:"",
      lco:'http://127.0.0.1:4000/',
      n:1,
      pic:"",
      title:"",
      // i:"",
      n:1,
      newuid:"",
      uid:"",
      newuid:"",
      way:"", //订单状态
      total:"",
      add:false,
      address:[]
    }
  },
  components:{
    MyAddress:Address
  },
  beforeCreate:function() {
    $("body")[0].style.background="#fff";
  },
  beforeDestroy:function(){
    $("body")[0].style.backgroundImage="-webkit-linear-gradient(top,#f3fbcc,#afe471)"
  },
  created(){
    this.load();
    this.selectAdd()
  },
  methods:{
    get(data){
      this.add=data
    },
    load(){
      this.pid=this.$route.query.pid;
      this.newuid=this.$route.query.newuid;
      this.pic=this.$route.query.pic;
      this.price=this.$route.query.price;
      this.uid=this.$route.query.uid;
      this.way=this.$route.query.way;
      this.title=this.$route.query.title;
      this.total=this.price;
      // var str=window.location.href;
      //    var arr=str.split("=");
      // if(str.indexOf("newuid")!=-1){
      //       //  console.log(arr)
      //     this.uid=arr[1].split("&")[0];
      //     this.newuid=arr[2].split("&")[0];
      //      this.pid=arr[3].split("&")[0];
      //      this.price=arr[4].split("&")[0];
      //      this.pic=arr[5].split("&")[0];
      //      this.i=arr[5].split("&")[1];      
      // }
      // else{
      // this.i=arr[3].split("&")[1];       
      // this.price=arr[2].split("&")[0];
      // this.pic=arr[3].split("&")[0];
      // this.pid=arr[1].split("&")[0]; 
      // var obj={pid:this.pid};
      // var url="product";
      // this.axios.get(url,{params:obj}).then(res=>{
      // this.title=res.data.data[this.pid-1].title
      // this.total=this.price;
      // })}
      //    var obj={pid:this.pid};
      //      var url="product";
      //      this.axios.get(url,{params:obj}).then(res=>{
      //      this.title=res.data.data[this.pid-1].title
      //      this.total=this.price;
      // })
    },
    pay(){
      if(this.way=="t"){
        var share_state=1;//拼单状态 1-待拼单 2-拼单成功  3-不拼单 4-拼单失败 5-拼单成功
      }else if(this.way=="o"){   
        var share_state=3;      
      }
      else {
        var share_state=5  
      }
     
    this.$messagebox({
       title:'提示',
       message:"确认支付？",
       showCancelButton: true
     }).then(()=>{
       if(this.$refs.dizhi.innerHTML=="手动添加收货地址"){
         this.$toast("请添加收货地址")
         this.add=true
       }else{
        var url="addcart"; 
        var time=`${new Date().getTime()}`;   
         var obj={pid:this.pid,count:this.n,price:this.price,order_time:time,share_state:share_state}
        this.axios.get(url,{params:obj}).then(res=>{ 
        if(res.data.code==1){
            this.$toast("支付成功")
            this.$router.push("/Orders");
          }
        })
       }
     })
      
    },
    num(i){
    var sub=document.querySelector(".sub");
    this.n=parseInt(this.n)
    this.n+=i;
    this.n==1&&(sub.style.background="#f2f2f2")
    this.n<1&&(this.n=1)
    this.n>1&&(sub.style.background="#ddd")
    this.total=(this.price*this.n).toFixed(2)
    },
    back(){
      this.$router.go(-1)
    },
    addAddress(){
      this.add=true
    },
    selectAdd(){
      var url="selectaddress";
      // var obj={uid:this.uid};
      // this.axios.get(url,{params:obj})
    this.axios.get(url)  .then(res => {
        this.address=res.data.data
        console.log(this.address)
      })
      .catch(err => {
        console.error(err); 
      })
    }
  }
}
</script>
<style scoped>
  .order{
    height:100%;
    position:fixed;
    background: #f5f5f5;
  }
  .top{
    width: 100%;
    height: 2.9rem;
    line-height: 2.9rem;
    background: #fff;
    border-bottom: 1px solid #ddd;
    padding: 0 .6rem;
    text-align: center;
    color: #333;
    font-size: .96rem;
  }
  .top i{
    float: left;
    font-size: 1.2rem
  }
  .address{
    height: 2.7rem;
    line-height: 2.7rem;
    background:#fff;
    padding: 0 0.63rem;
    font-size: .9rem
  }
  .address i.add{
    background: url(../../assets/add.png) no-repeat;
    background-size: 100%;
    display:inline-block;
    width: 1.1rem;
    height: 1.1rem;
    position: relative;
    top: 0.2rem;
    margin-right: .6rem;
  }
  .address i.skip{
    background: url(../../assets/skip.png) no-repeat;
    background-size: 100%;
    display:inline-block;
    width: .75rem;
    height: .75rem;
    opacity: .3;
    position: relative;
    left: 55%;
  }
  .line{
    background: url(../../assets/line.png) no-repeat;
    background-size: 100%;
    width: 100%;
    height: 0.1rem;
  }
  .img{
    width: 5.7rem;
    height: 5.7rem;
    margin-right: 0.625rem;
  }
  .product{
    display: flex;
    padding: 0.6rem .75rem;
  }
  .details{
    position: relative;
    padding: 0.6rem 0;
  }
  .details p.title{
    font-size: .81rem;
    width: 15.62rem;
    max-height: 2rem;
    line-height: 1rem;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical
  }
  .details p.price{
    position: absolute;
    bottom: 0;
    font-size: .88rem;
  }
  .num{
    height: 3rem;
    line-height: 3rem;
    background: #fff;
    display: flex;
    padding-left: 0.75rem;
    position: relative;
  }
  .num>div{
    position: absolute;
    right: 1.5rem;
  }
  .num button{
    border: 0;
    outline: none;
    width: 2rem;
    height: 1.56rem;
    border-radius: .13rem;
    color: #58595b;
  }
  .num button.sub{
    background: #f2f2f2;
  }
  .num>div input{
    width: 0.625rem;
    min-width: 1.81rem;
    border: 0;
    outline: none;
    text-align: center
  }
  .bottom{
    width: 100%;
    position: absolute;
    bottom: 4.4rem;
    font-size: .75rem;
    color: #9c9c9c;
    display: flex;
    justify-content: center;
    align-items: center
  }
  .bottom div{
    background: url(../../assets/picc_v2.png) no-repeat;
    background-size: 100%;
    display: inline-block;
    width: 5.44rem;
    height: 0.75rem;
    margin: 0.17rem 0.07rem 0;
  }
  .pay{
    width: 100%;
    height: 3.4rem;
    line-height: 3.4rem;
    position: fixed;
    bottom: 0;
    display: flex;
    background: #fff;
    border-top: 1px solid #e0e0e0
  }
  .pay p{
    font-size: .88rem;
    width: 64%;
    text-align: right;
  }
  .pay p span{
    color: #e02e24
  }
  .pay p span.price{
    font-size: 1.25rem;
    margin-right: 0.2rem;
  }
  .pay .btn{
    width: 7.5rem;
    background: #e02e24;
    color: #fff;
    text-align: center;
    font-size: 1.13rem;
    position: absolute;
    right: 0;
  }
  .show_add{
    width: 100%;
    min-height: 4.625rem;
    background: #fff;
    display: flex;
    align-items: center;
    justify-content: space-around;
    color: #151516;
    font-size: .813rem
  }
  .show_add i.position{
    background: url(../../assets/shouhuodizhi.png) no-repeat;
    background-size:100%;
    display: inline-block;
    width: 1.375rem;
    height: 1.375rem;
  }
  .show_add i.more{
    background: url(../../assets/skip.png) no-repeat;
    background-size:100%;
    display: inline-block;
    width: .75rem;
    height: .75rem;
    opacity: .3;
  }
  .show_add .information{
    width: 18.125rem;
  }
  .show_add .name{
    font-weight: 700;
    font-size: 1rem;
    margin-right: 0.75rem;
  }
  .show_add .phone{
    font-size: .875rem
  }
</style>
