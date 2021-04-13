<template>
  <div class="swiper">
    <div class="indicator" v-if="showIndicator && slideCount>1">
      <ul>
        <li v-for="(item, index) in slideCount" :key="index" @click="setPosition(index)">
          <div :class="{active: index === currentIndex }"></div>
        </li>
      </ul>
    </div>
    <div :class="{'item': true, 'noItem': index != leaveIndex && index != currentIndex}" v-for="(item, index) in itemData" :key="index">
      <div :class="{'item-main': true, 'enterMainItem': index === enterIndex, 'leaveMainItem': index === leaveIndex}" :style="{backgroundImage:'url(' + item.mainBgImg + ')'}">
        <img class="img"  :src="item.mainImg">
      </div>
      <div :class="{'item-bg': true, 'enterItem': index === enterIndex, 'leaveItem': index === leaveIndex}">
        <div class="img" :style="{backgroundImage: 'url(' + item.bgImg + ')'}"></div>
        <div class="color" :style="{backgroundColor: item.bgColor}"></div>
      </div>
      <div class="item-label"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Swiper',
  props: {
     interval: {//自动播放时间间隔
	    type: Number,
       default: 8000
     },
     leaveTime: {//自动播放时间间隔
	    type: Number,
       default: 3000
     },
     showIndicator: {
       type: Boolean,
       default: true
     }
  },
  data: function () {
		  return {
        slideCount: 0, //元素个数
        swiperWidth: 0, //swiper的宽度
        currentIndex: 0, //当前的index
        scrolling: false, //是否正在滚动
        enterIndex: null, //将要展示的图片
        leaveIndex: null, //即将展示完毕的图片
        itemData: [
          {
            mainImg: require("../../assets/img/img_slide_04.ff41772.jpg"), 
            mainBgImg: require("../../assets/img/bg_slide_00.ba0d2b2.jpg"), 
            bgImg: require("../../assets/img/bg_net_pink.71f6e3d.svg"), 
            bgColor: "#ffc9ad",
          },
          {
            mainImg: require("../../assets/img/img_slide_04.ff41772.jpg"), 
            mainBgImg: require("../../assets/img/bg_slide_01.f7b75cb.jpg"), 
            bgImg: require("../../assets/img/bg_net_pink.71f6e3d.svg"), 
            bgColor: "#ffe200",
          },
          {
            mainImg: require("../../assets/img/img_slide_04.ff41772.jpg"), 
            mainBgImg: require("../../assets/img/bg_slide_02.312ad9c.jpg"), 
            bgImg: require("../../assets/img/bg_net_pink.71f6e3d.svg"), 
            bgColor: "#ffeace",
          },
          {
            mainImg: require("../../assets/img/img_slide_04.ff41772.jpg"), 
            mainBgImg: require("../../assets/img/bg_slide_04.bb6d3a2.jpg"), 
            bgImg: require("../../assets/img/bg_net_pink.71f6e3d.svg"), 
            bgColor: "#e593c8",
          }
        ]
      }
    },
  mounted: function() {
    this.handleDom();
  },
  methods: {
    /**
    * 获取DOM, 在DOM后添加Slide
    */
    handleDom: function() {
      // 1.获取要操作的元素
      const swiper = document.querySelector(".swiper");
      const swiperEls = document.getElementsByClassName("item");

      // 2.获取长度和swiper宽度
      this.slideCount =  swiperEls.length;
      this.swiperWidth = swiper.offsetWidth;

      //鼠标经过swiper停止定时器
      swiper.addEventListener("mouseenter", () => {
        clearInterval(this.timer);
        this.timer = null; //清除定时器变量
      })

      //鼠标离开swiper开启定时器
      swiper.addEventListener("mouseleave", () => {
        this.antoTransfrom();
      })

      this.antoTransfrom();
    },

    //自动滚动
    antoTransfrom: function() {
      this.timer = setInterval(() => {
        this.leaveIndex = this.currentIndex;
        this.currentIndex++;
        this.enterIndex = this.currentIndex;
        if(this.currentIndex === this.slideCount) {
          this.currentIndex = 0;
          this.enterIndex = 0;
        } 
        setTimeout(() => {
           this.leaveIndex = null;
        },this.leaveTime)
      }, this.interval)
    },

    //点击跳转到对应页面
    setPosition: function(index) {
      this.currentIndex = index; //确保自动滚动从该索引号开始
    }
  }
} 
</script>

<style lang="scss" scoped>
 .swiper {
    position: relative;
    width: 100%;
    height: 100%;
    overflow: hidden;
  }
  .indicator {
    position: absolute;
    width: 100%;
    height: 10%;
    z-index: 3;
    ul {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100%;
      padding: 0px;
      margin: 0px;
      li {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 5%;
        list-style: none;
        div {
          width: 90%;
          height: 0.05rem;
          background: #666;
        }
        .active {
          height: 0.1rem;
          background: #333;       
        }
      }
    }
  }
  .noItem {
    display: none;
  }
  .enterItem {
    z-index: 2;
    animation: changeWidth 3s;
  }
  .leaveItem {
    z-index: 1;
    animation: rotatey 3s;
    transform-origin: 100% 50%;
  }
  .enterMainItem {
    z-index: 2;
    animation: changeMainWidth 3s;
  }
  .leaveMainItem {
    z-index: 1;
    animation: rotatey 1.5s;
    transform-origin: 100% 50%;
  }
  
  .item {
    position: absolute;
    width: 100%;
    height: 100%;
    .item-bg {
      position: absolute;
      width: 100%;
      height: 100%;
      z-index: 1;
      .img {
        position: absolute;
        width: 100%;
        height: 100%;
        opacity: .6;
        z-index: 1;
        animation: movebg 20s;      
      }
      .color {
        position: absolute;
        width: 100%;
        height: 100%;
      }
    }
   .item-main {
      position: absolute;
      display: flex;
      justify-content: center;
      left: 15%;
      top: 10%;
      width: 70%;
      height: 72%;
      z-index: 2;
      .img {
        margin: 0 auto;
        height: 100%;
      }
   }
 }

 @keyframes movebg {
    0% {
      transform: scale(0px);
    }
    10% {
      transform: scale(1.05, 1);
    }
    100% {
      transform: scale(1.05, 1) translateX(50px);
    }
 } 

 @keyframes changeWidth {
    0% {
      width: 0%;
    }
    50% {
      width: 100%;
    }
 } 

 @keyframes changeMainWidth {
    0% {
      width: 0%;
    }
    50% {
      width: 70%;
    }
 } 

  @keyframes rotatey {
     0% {
      transform: rotateY(0deg);
    }
    100% {
      transform: rotateY(90deg);
    }
 } 
</style>