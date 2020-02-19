<template>
  <div class="search">
    <div class="ss">
      <i class="back" @click="back"></i>
      <div class="ss-in">
        <i class="mintui mintui-search"></i>
        <input type="text" placeholder="苹果" v-model="s" ref="input" />
      </div>
      <span @click="search">搜索</span>
    </div>
    <div class="main">
      <div class="history">
        <p>
          历史搜索
          <i class="del" @click="del"></i>
          </p>
        <span>牛奶</span>
        <span>香蕉</span>
      </div>
      <!-- <div class="found">
        <p>搜索发现</p>
        <span>牛奶</span>
        <span>鸡蛋</span>
        <span>黄瓜</span>
        <span>玉米</span>
        <span>青椒</span>
        <span>番茄</span>
        <span>泡面</span>
        <span>冬瓜</span>
        <span>香蕉</span>
        <span>葱</span>
        <span>豆腐</span>
        <span>土豆</span>
        <span>鸡翅</span>
        <span>西葫芦</span>
        <span>虾</span>
      </div> -->
      <!-- <div class="wrap">
        <div class="recommend-item" v-for="(item,i) of list" :key="i" >
          <div>
            <img :src="'http://127.0.0.1:4000/'+item.pic" @click="examine"  :data-pid="item.pid">
            <div>
              <span class="recommend-title">{{item.title}}</span>
              <span class="recommend-price">¥{{item.price}}</span>        
            </div>
          </div>
        </div>
      </div> -->
      <div class="details" v-if="show">
        <div v-for="(item,i) of list" :key="i">
          <img :src="'http://127.0.0.1:4000/'+item.pic" alt="" />
          <div>
            <span>{{item.title}}</span>    
            <span>¥{{item.price}}</span> 
          </div>           
        </div>
      </div>
      <div class="no" v-else>
        <div>
          <img src="../../assets/icon/search.png" alt="">
        </div>
         <p>没有找到相关宝贝!</p>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data(){
    return{
      list:[],
      bt:"",
      s:"",
      show:true,
    }
  },
  mounted(){
    this.loadMore();
  },
  methods:{
    loadMore(){
      
    },
    back(){
      document.querySelector(".search").style.display="none";
    },
    del(){
      document.querySelector(".history").remove()
    },
    search(){
      var url="search";
      var input=this.$refs.input
      if(!input.value){
        this.s=input.placeholder;
      }
      var obj={bt:this.s};
      this.axios.get(url,{params:obj}).then(res=>{
        if(res.data.code==1){
          this.list=res.data.data;
          this.show=true
        }else{
           this.show=false
          }
      })
    }
  }
}

</script>
<style scoped>
  .search{
    width: 100%;
    height: 100%;
    position: fixed;
    left: 0;
    top: 0;
    z-index: 2;
    background: #f2f2f2;
    display: none;
  }
  .ss{
    width: 100%;
    height: 2.9rem;
    background-color: #73ac91;
    display: flex;
    padding: .3rem;
    align-items: center;
    justify-content: space-between
  }
  .ss .back{
    background: url("../../assets/back.png") no-repeat;
    background-size: 100%;
    display: block;
    width: 35px;
    height: 35px;
  }
  .ss-in{
    background: #fff;
    width: 77%;
    border-radius: 1.875rem;
    padding: 0 1rem;
    position: relative;
  }
  .mintui-search:before{
    color: #d9d9d9
  }
  .ss-in input{
    border: 0;
    outline: none;
    padding: 0.4rem 1.3rem;
    -webkit-text-fill-color: #999
  }
  .ss-in .mintui-search{
    position: absolute;
    top: 0.4rem;
    left: 0.9rem;
  }
  .ss span{
    color: #fff;
    font-size: .9rem;
    margin: 0 .5rem;
  }
  .main{
    padding: 0 .8rem;
  }
  .main p{
    color: #222;
    font-size: .9rem;
    margin: 1rem 0;
    position: relative;
  }
  .history span{
    display: inline-block;
    background: #fff;
    border: 1px solid #ddd;
    border-radius: .9rem;
    color: #777;
    padding: 0.4rem .7rem;
    font-size: .5rem;
    margin-right: 0.5rem;
  }
  .main .found span{
    margin-bottom: 0.6em;
  }
  .main .del{
    background: url(../../assets/del.png) no-repeat;
    background-size: 100%;
    display: inline-block;
    width: 1rem;
    height: 1rem;
    position: absolute;
    top: 0;
    right: 0;
  }
  .details{
    display: flex;
    justify-content: start;
    margin-top: 1rem;
    flex-wrap: wrap;
    
  }
  .details>div{
    width: 48%;
    margin: 0 .2rem .5rem;
    font-size:.8rem;
    background: #fff;
    border-radius:9px; 
  }
  .details img{
    width: 100%;
    border-top-left-radius:9px;
    border-top-right-radius: 9px; 
  }
   .details span{
     display: inline-block;
   }
  .details span:last-child{
    color:#f13f09;
    margin: 0.5rem 0.5rem;
  }
  .details span:first-child{
    overflow: hidden;
    flex-wrap: nowrap;
    height: 1rem;
    line-height: 1.2rem;
    margin-left:0.5rem; 
    /* font-size: */
  }
  .no{
    width: 100%;
    height: 15rem;
    
  }
  .no>div{
    width: 6rem;
    height: 6rem;
    margin: 2rem auto;
  }
  .no img{
   width: 100%;
  }
  .no p{
    text-align: center;
    color: #d7d8da;
    font-size:1.5rem 
  }
</style>
