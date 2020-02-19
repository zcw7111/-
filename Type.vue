<template>
  <div class="type">
    <ul>
      <li>
        <a @click="tab(1)">
          <img src="../../assets/01.png">
          <span>蔬菜豆制品</span>
        </a>
      </li>
      <li>
        <a @click="tab(2)">
          <img src="../../assets/02.png">
          <span>当季水果</span>
        </a>
      </li>
      <li>
        <a @click="tab(3)">
          <img src="../../assets/03.png">
          <span>水产海鲜</span>
        </a>
      </li>
      <li>
        <a @click="tab(4)">
          <img src="../../assets/04.png">
          <span>乳品粮油</span>
        </a>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  methods:{
    tab(key){
      this.$router.push("/Class?id="+key)
    }
  }
}
</script>

<style scoped>
  .type{
    background: #fff;
    padding: .5rem 0;
  }
  .type ul{
    width: 100%;
    display: flex
  }
  .type img{
    width: 3rem;
    height: 3rem;
  }
  .type li{
    width: 25%;
    text-align: center;
  }
  .type span{
    display: block;
    font-size: .75rem;
    color: #666;
  }
</style>
