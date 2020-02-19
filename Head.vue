<template>
  <div class="head">
    <div class="head-in" @click="search">
      <i class="mintui mintui-search"></i>
      <span>输入商品名称</span>
    </div>
  </div>
</template>
<script>
export default {
  data(){
    return{
      
    }
  },
  methods:{
    search(){
      document.querySelector(".search").style.display="block";
    }
  },
}
</script>
<style scoped>
  .head{
    width: 100%;
    position: sticky;
    top: 0;
    z-index: 1;
    background:#91c7ae;
    padding:.5rem .875rem;
  }
  .head-in{
    background:#fff;
    border-radius: 1.875rem;
    height: 2rem;
    line-height: 1.9rem;
    text-align: center;
    font-size: .16rem;
  }
  .head-in i::before{
    font-size: .16rem;
    margin-right: .4rem;
  }
  .head-in span{
    color: #666
  }
</style>
