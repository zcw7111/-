<template>
  <div>
    <mt-tabbar fixed v-model="active"> 
      <mt-tab-item :id="0==j?active:''" @click.native="changeState(0)">
        <tabbaricon slot="icon" :focused="currentIdx[0].isSelect" :selectedImage="require('../../assets/home_selected.png')" :normalImage="require('../../assets/home.png')"></tabbaricon>
        首页
      </mt-tab-item>
      <mt-tab-item :id="1==j?active:''" @click.native="changeState(1)">
        <tabbaricon slot="icon"  :focused="currentIdx[1].isSelect" :selectedImage="require('../../assets/classify_selected.png')" :normalImage="require('../../assets/classify.png')"></tabbaricon>
        分类
      </mt-tab-item>
      <mt-tab-item :id="2==j?active:''" @click.native="changeState(2)">
        <tabbaricon slot="icon"  :focused="currentIdx[2].isSelect" :selectedImage="require('../../assets/chat_selected.png')" :normalImage="require('../../assets/chat.png')"></tabbaricon>
        聊天
      </mt-tab-item>
      <mt-tab-item :id="3==j?active:''"  @click.native="changeState(3)">
        <tabbaricon slot="icon"  :focused="currentIdx[3].isSelect" :selectedImage="require('../../assets/mine_selected.png')" :normalImage="require('../../assets/mine.png')"></tabbaricon>
        我的
      </mt-tab-item>
    </mt-tabbar>
  </div>
</template>
<style scoped>
  .mint-tabbar>.mint-tab-item.is-selected{
    background-color: transparent;
    color: #45c018
  }
  .mint-tabbar>.mint-tab-item{
    color: #999
  }
</style>
<script>
import TabBaricon from "./TabBaricon.vue"
export default {
  data(){
   return{
     active:"0",
     currentIdx:[    //下面数组保存按钮状态
      {isSelect:true},
      {isSelect:false},
      {isSelect:false},
      {isSelect:false},
    ],
    idx:this.j
    }
  },
  props:{
    j:""
  },
  created(){
    this.change(this.idx)
  },
  components:{
    "tabbaricon":TabBaricon
  },
  methods:{
    change(j){
      for(var i=0;i<this.currentIdx.length;i++){
        if(i==j){
            this.currentIdx[i].isSelect=true
        }else{
            this.currentIdx[i].isSelect=false
        }
      }
    },
    changeState(i){
      this.active=i;
      switch (i) {
        case 0:
          this.$router.push("/")
          break;
        case 1:
          this.$router.push("/Class")
          break;
        case 2:
          this.$router.push("/Chat")
          break;
        case 3:
        this.$router.push("/Mine");
        break;
      }
    },
  }
}
</script>