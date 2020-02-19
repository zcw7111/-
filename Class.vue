<template>
  <div>
    <search></search>
    <my-head></my-head>
    <div class="swiper-container">
      <div class="swiper-wrapper">
        <div class="main">
          <div class="left">
            <ul>
              <li v-for="(item1, k1) in items1" :key="k1" @click="left_click($event)">{{ item1 }}</li>
            </ul>
          </div>
          <div class="right">
            <ul>
              <li v-for="(item2, k2) in items2" :key="k2">
                <h4>{{item2.class}}</h4>
                <div v-for="(item3, k3) in item2.list" :key="k3" class="content">
                  <div class="item">
                    <img :src="item3.img">
                    <div class="title">{{ item3.title }}</div>
                  </div>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
    <foot :j="j"></foot>
  </div>
</template>

<script>
import BScroll from 'better-scroll';
import Foot from './Foot.vue'
export default {
  data() {
    return {
      j:1,
      items1:["热门推荐","安心蔬菜","豆制品","新鲜水果","肉禽蛋","海鲜水产","乳品烘焙","米面粮油","火锅来了","营养早餐","调味品"],
      items2:[
        {
          class:'热门推荐',
          list:[{title:'虾',img:"../../../static/shrimp.jpg"},{title:'苹果',img:"../../../static/apple.jpg"},{title:'食用油',img:"../../../static/oil.jpg"},{title:'豆制品',img:"../../../static/bean.jpg"},{title:'米',img:"../../../static/trepang.png"},{title:'海参',img:"../../../static/shrimp.jpg"}]
        },
        {
          class:'安心蔬菜',
          list:[{title:'土豆',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'番薯',img:"../../../static/fs.jpg"},{title:'芋头',img:"../../../static/yt.jpg"},{title:'玉米',img:"../../../static/ym.jpeg"},{title:'番茄',img:"../../../static/tomato.jpg"},{title:'山药',img:"../../../static/8986cf6f-6b60-4dfd-bcda-2d03f4637fc4.jpg"}]
        },
        {
          class:'豆制品',
          list:[{title:'土豆',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'番薯',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'芋头',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'玉米',img:"../../../static/ym.jpeg"},{title:'番茄',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'山药',img:"../../../static/8986cf6f-6b60-4dfd-bcda-2d03f4637fc4.jpg"}]
        },
        {
          class:'新鲜水果',
          list:[{title:'百香果',img:"../../../static/bxg.jpg"},{title:'苹果',img:"../../../static/2a9d7030-0061-4171-9c91-1c3e47bfbed7.jpg"},{title:'火龙果',img:"../../../static/bbd35225-f7d8-46b3-ae15-ee8b56f64ae7.jpg"},{title:'枣',img:"../../../static/b80436be-b48e-4013-9a4a-ab5bcff231b1.jpg"},{title:'榴莲',img:"../../../static/7241c5cb-9c97-4352-a1c4-88e513554d3e.jpg"},{title:'芒果',img:"../../../static/mg.jpg"}]
        },
        {
          class:'肉禽蛋',
          list:[{title:'土豆',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'番薯',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'芋头',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'玉米',img:"../../../static/ym.jpeg"},{title:'番茄',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'山药',img:"../../../static/8986cf6f-6b60-4dfd-bcda-2d03f4637fc4.jpg"}]
        },
        {
          class:'海鲜水产',
          list:[{title:'海参',img:"../../../static/shrimp.jpg"},{title:'海带',img:"../../../static/hd.jpg"},{title:'八爪鱼',img:"../../../static/bzy.jpg"},{title:'螃蟹',img:"../../../static/px.jpeg"},{title:'甲鱼',img:"../../../static/jy.jpeg"},{title:'虾',img:"../../../static/shrimp.jpg"}]
        },
        {
          class:'乳品烘焙',
          list:[{title:'虾',img:"../../../static/shrimp.jpg"},{title:'苹果',img:"../../../static/apple.jpg"},{title:'食用油',img:"../../../static/oil.jpg"},{title:'豆制品',img:"../../../static/bean.jpg"},{title:'米',img:"../../../static/trepang.png"},{title:'海参',img:"../../../static/shrimp.jpg"}]
        },
        {
          class:'米面粮油',
          list:[{title:'百香果',img:"../../../static/bxg.jpg"},{title:'苹果',img:"../../../static/2a9d7030-0061-4171-9c91-1c3e47bfbed7.jpg"},{title:'火龙果',img:"../../../static/bbd35225-f7d8-46b3-ae15-ee8b56f64ae7.jpg"},{title:'枣',img:"../../../static/b80436be-b48e-4013-9a4a-ab5bcff231b1.jpg"},{title:'榴莲',img:"../../../static/7241c5cb-9c97-4352-a1c4-88e513554d3e.jpg"},{title:'芒果',img:"../../../static/2a9d7030-0061-4171-9c91-1c3e47bfbed7.jpg"}]
        },
        {
          class:'火锅来了',
          list:[{title:'土豆',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'番薯',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'芋头',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'玉米',img:"../../../static/ym.jpeg"},{title:'番茄',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'山药',img:"../../../static/8986cf6f-6b60-4dfd-bcda-2d03f4637fc4.jpg"}]
        },
        {
          class:'营养早餐',
          list:[{title:'土豆',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'番薯',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'芋头',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'玉米',img:"../../../static/ym.jpeg"},{title:'番茄',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'山药',img:"../../../static/8986cf6f-6b60-4dfd-bcda-2d03f4637fc4.jpg"}]
        },
        {
          class:'调味品',
          list:[{title:'土豆',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'番薯',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'芋头',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'玉米',img:"../../../static/ym.jpeg"},{title:'番茄',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'山药',img:"../../../static/8986cf6f-6b60-4dfd-bcda-2d03f4637fc4.jpg"},{title:'土豆',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'番薯',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'芋头',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'玉米',img:"../../../static/ym.jpeg"},{title:'番茄',img:"../../../static/94a88468-b63b-4195-af35-41cb62d86b86.jpg"},{title:'山药',img:"../../../static/8986cf6f-6b60-4dfd-bcda-2d03f4637fc4.jpg"}]
        }
      ],
      id:""
    };
  },
  components:{
    Foot
  },
  created() {
    this.scroll_init();
    this.load()
  },
  mounted(){
    $('.left ul li').first().addClass('selected');
    $(".right ul li").last().css("padding-bottom","11.5rem")
  },
  methods: {
    scroll_init: function() {    
      $(window).scroll(function() {
        // 这里在滚动的时候做监听,如果翻上去的部分超过0的时候，切换商品和左侧这里做绝对定位
        if ($(window).scrollTop() >= 0) {
          $('.left').css('position', 'fixed');
        } else{
          $('.left').css('position', '');
        }
        // 获取右侧当前li距离顶端的高度 - 右侧已经翻上去的高度 - head的高度
        $('.right ul li').each(function() {
          var target = parseInt($(this).offset().top - $(window).scrollTop()-180);
          var i = $(this).index();
          // if target<=0 清除所又li的active, 给当前li赋予active
          if (target <= 0) {
            $('.left ul li').removeClass('selected');
            $('.left ul li').eq(i).addClass('selected');
          }
        });
      });
      // 点击左侧li通过下标找到相应li的位置，通过animate滚动到相应的位置
      $('.left ul li').click(function() {
        var i = $(this).index('.left ul li');
        $('body,html').animate({
          scrollTop: $('.right ul li').eq(i).offset().top - 180
        },1000);
      });
    },
    left_click: function (e) {
      //e.srcElement,,表示触发点击事件的当前盒子元素DOM
      var i = $(e.srcElement).index('.left ul li');
      $('body,html').animate({
        scrollTop: $('.right ul li').eq(i).offset().top - 50
      },1000);
    },
    load(){
      var str=window.location.href;
      var id=str.split("=")[1];
      if(id==1){
        $("body,html").animate({
          scrollTop:258
        },false);
      }else if(id>1){
         $("body,html").animate({
          scrollTop:258+(id-1)*244*2
        },false);
      }
    }
  }
};
</script>

<style scoped>
  .main{
    width: 100%;
    font-size: .875rem;
    overflow: hidden;
  }
  .left{
    width: 5.38rem;
    height: 100%;
    float: left;
    background: #f7f7f7;
    overflow: hidden;
  }
  .left ul{
    width: 5.31rem;
  }
  .left li{
    padding: 1rem 0;
    background: #f6f6f6;
    text-align: center;
    color: #333;
  }
  .left li.selected{
    background: #fff;
    color: #e93b3d
  }
  .right{
    width: 18.06rem;
    height: 100%;
    background:#fff;
    margin-left: 5.375rem;
  }
  .right ul{
    padding: 1rem .625rem 0;
  }
  .right li{
    font-size: .75rem;
    color: #333;
    padding: 0.5rem 0;
  }
  .right li h4{
    font-size: .875rem;
    margin-bottom: 0.5rem;
  }
  .right .content{
    display: inline-block;
    width: 33.3%;
    text-align: center
  }
  .right .item{
    margin: .5rem 0;
  }
  .right li img{
    width: 4.1rem;
    height: 4.1rem;
  }
</style>