<template>
  <div class="rec">
    <div class="head">
      <img src="../../assets/heart.png">
      <span>猜你喜欢</span>
    </div>
    <div class="wrap">
      <div class="recommend-item" v-for="(item,i) of list" :key="i"  >
        <div>
          <img :src="'http://127.0.0.1:4000/'+item.pic" @click="examine"  :data-pid="item.pid">
          <div>
            <span class="recommend-title">{{item.title}}</span>
            <span class="recommend-price">¥{{item.price}}</span>        
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
  .rec .head{
    height: 2.5rem;
    text-align: center;
    line-height: 2.5rem;
  }
  .rec .head img{
    width: 1.2rem;
    position: relative;
    right: 0.5rem;
    top: 0.25rem;
  }
  .rec .head span{
    font-size: .96rem;
    color: #c23531
  }
  .wrap{
    width: 100%;
    display: flex;
    flex-flow: wrap;
    padding: 0 .4rem;
  }
  .wrap .recommend-item{
    width: 48%;
    background: #fff;
    margin: 0 .2rem 0.5rem;
    font-size: .8rem;
    border-radius: 9px;
  }
  .wrap img{
    width: 100%;
    border-radius: 9px 9px 0 0;
  }
  .wrap span{
    display: block;
    color: #333;
  }
  .wrap .recommend-title{
    height: 1rem;
    line-height: 1.2rem;
    overflow: hidden;
  }
  .wrap .recommend-price{
    color: #61b724;
    margin: 0.5rem 0;
    font-size: .95rem
  }
  .wrap .recommend-item>div>div{
    padding-left: 0.3rem;
  }
</style>
<script>
export default {
  data(){
    return{
      list:[],
      pno:0,
    }
  },
  created() {
    this.loadMore();
  },
  mounted(){
    window.addEventListener("scroll",this.handleScroll)
  },
  beforeDestroy(){
    window.removeEventListener("scroll",this.handleScroll)
  },
  methods:{
    examine(e){
        //验证是否登录
      var pid = e.target.dataset.pid;
      var url="verify";
      this.axios.get(url).then(res=>{{
        if(res.data.code==-1){
          this.$router.push('/LoginReg')
        }else{
          this.$router.push(`/details?pid=${pid}`); 
        }
      }})
    },
    loadMore(){
      var url="product";
      this.pno++;
      var obj={pno:this.pno};
      this.axios.get(url,{params:obj}).then(res=>{
        var rows=this.list.concat(res.data.data);
        this.list=rows;
      })
    },
    handleScroll(){
      //是否滚动到底部的判断
      if((document.documentElement.scrollTop+window.innerHeight)==document.body.offsetHeight){
        this.loadMore()
      }
    }
  }
}
</script>