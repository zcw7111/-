<template>
  <div class="car">
    <mt-swipe>
      <mt-swipe-item><img src="../../assets/cse1.jpg"></mt-swipe-item>
      <mt-swipe-item><img src="../../assets/cse2.jpg"></mt-swipe-item>
      <mt-swipe-item><img src="../../assets/cse3.jpg"></mt-swipe-item>
      <mt-swipe-item><img src="../../assets/cse4.jpg"></mt-swipe-item>
    </mt-swipe>
  </div>
</template>

<style scoped>
  .car{
    height: 10rem;
  }
  .car img{
    width:100%;
    height:100%;
  }
  .car >>> .mint-swipe-indicator{
    background: #fff;
    opacity: .9;
    width: .25rem;
    height: 0.25rem;
  }
  .car >>> .mint-swipe-indicator.is-active{
    background: #43a148
  }
</style>
