<template>
  <div class="chat">
    <div class="chat-list">
      <div class="chat-list-msg">
        <div class="avatar"><img src="../../assets/logo.jpg"></div>
        <div class="detail">
          <div class="name">
            <span>惠生活官方客服</span>
            <p>官方</p>
            <span class="time">08:19</span>
          </div>
          <p>亲，中午好，记得好好吃饭哟，您想问多多什么问题呢？</p>
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
      j:2
    }
  },
  components:{
    Recommend,
    Foot
  }
}
</script>
<style scoped>
  .chat-list{
    background: #fff;
  }
  .chat-list-msg{
    display: flex;
    padding: 0.8rem;
  }
  .avatar img{
    width: 3rem;
    height: 3rem;
    border-radius: 50%
  }
  .chat-list-msg .name{
    display: flex;
    position: relative;
  }
  .chat-list-msg .name span{
    font-size: 1rem;
    color: #333;
  }
  .chat-list-msg .name p{
    height: 1rem;
    line-height: 1rem;
    font-size: .6rem;
    color: #e02e24;
    border: 1px solid #e02e24;
    margin: .3rem .4rem;
    padding: 0 .2rem;
  }
  .chat-list-msg .name .time{
    position: absolute;
    right: 0;
    font-size: .75rem;
    color: #bbb
  }
  .chat-list-msg .detail{
    width: 80%;
    margin-left: 0.75rem;
    line-height: 1.6rem;
  }
  .chat-list-msg .detail>p{
    font-size: .8rem;
    color: #999;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
</style>
