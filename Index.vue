<template>
  <div>
    <search></search>
    <div class="index">
      <my-head></my-head>
      <carousel></carousel>
      <type></type>
      <keep-alive>
        <recommend></recommend>
      </keep-alive>
      <foot :j="j"></foot>
    </div>
  </div>
</template>
<script>
import Carousel from './Carousel.vue'
import Type from './Type.vue'
import Recommend from './Recommend.vue'
import Foot from './Foot.vue'
export default {
  data(){
    return{
      j:0,
    }
  },
  components:{
    Carousel,
    Type,
    Recommend,
    Foot
  },
}
</script>
<style scoped>
  .index{
    min-height: 100%
  }
</style>
