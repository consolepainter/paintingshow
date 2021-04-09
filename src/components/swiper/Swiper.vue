<template>
  <div class="swiper">
    <div class="indicator" v-if="showIndicator && slideCount>1">
      <ul>
        <li v-for="(item, index) in slideCount" :key="index" @click="setPosition(index)">
          <div :class="{active: index === currentIndex}"></div>
        </li>
      </ul>
    </div>
    <div class="content">
      <div class="item" v-for="(item, index) in itemData" :key="index">
        <div class="item-main" :style="{backgroundImage:'url(' + item.mainBgImg + ')'}">
          <img class="img" :src="item.mainImg">
        </div>
        <div class="item-bg">
          <div class="img" :style="{backgroundImage: 'url(' + item.bgImg + ')'}"></div>
          <div class="color" :style="{backgroundColor: item.bgColor}"></div>
        </div>
        <div class="item-label"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Swiper',
  props: {
     interval: {//自动播放时间间隔
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
        slideCount: 0, // 元素个数
        swiperWidth: 0, // swiper的宽度
        swiperStyle: {}, // swiper样式
        currentIndex: 0, // 当前的index
        scrolling: false, // 是否正在滚动
        itemData: [
          {
            mainImg: require("../../assets/img/img_slide_04.ff41772.jpg"), 
            mainBgImg: require("../../assets/img/bg_slide_04.bb6d3a2.jpg"), 
            bgImg: require("../../assets/img/bg_net_pink.71f6e3d.svg"), 
            bgColor: "#e593c8",
          },
          {
            mainImg: require("../../assets/img/img_slide_04.ff41772.jpg"), 
            mainBgImg: require("../../assets/img/bg_slide_04.bb6d3a2.jpg"), 
            bgImg: require("../../assets/img/bg_net_pink.71f6e3d.svg"), 
            bgColor: "#e593c8",
          },
          {
            mainImg: require("../../assets/img/img_slide_04.ff41772.jpg"), 
            mainBgImg: require("../../assets/img/bg_slide_04.bb6d3a2.jpg"), 
            bgImg: require("../../assets/img/bg_net_pink.71f6e3d.svg"), 
            bgColor: "#e593c8",
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
      const swiperEl = document.querySelector(".content");
      const swiperEls = swiperEl.getElementsByClassName("item");

      // 2.获取长度和swiper宽度
      this.slideCount =  swiperEls.length;
      this.swiperWidth = swiper.offsetWidth;

      // 3.如果大于1个, 那么在前后分别添加一个slide
      if(this.slideCount > 1) {
        const cloneFirst = swiperEls[0].cloneNode(true);
        //const cloneLast = slidesEls[this.slideCount - 1].cloneNode(true);
        swiperEl.appendChild(cloneFirst);
        //swiperEl.insertBefore(cloneLast, slidesEls[0]);
      }

      //鼠标经过swiper停止定时器
      swiper.addEventListener("mouseenter", () => {
        clearInterval(this.timer);
        this.timer = null; //清除定时器变量
      })

      //鼠标离开swiper开启定时器
      swiper.addEventListener("mouseleave", () => {
        this.antoTransfrom(this.swiperWidth);
      })

      this.antoTransfrom(this.swiperWidth);
    },

    //自动滚动
    antoTransfrom: function(swiperWidth) {
      const content = document.querySelector(".content");
      this.timer = setInterval(() => {
        this.currentIndex++;
        if(this.currentIndex == this.slideCount + 1) {
          content.style.left = 0;
          this.currentIndex = 0;
          content.style.transition = "none";
        } 
        else {
          content.style.transition = "all .3s";
        }
        const translatex = -this.currentIndex * swiperWidth;
        content.style.transform = "translateX(" + translatex + "px)";
      }, this.interval)
    },

    //点击跳转到对应页面
    setPosition: function(index) {
      this.currentIndex = index; //确保自动滚动从该索引号开始
      const content = document.querySelector(".content");
      const translatex = -index * this.swiperWidth;
      content.style.transition = "all .3s";
      content.style.transform = "translateX(" + translatex + "px)";
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
  .content {
    position: absolute;
    display: flex;
    width: 500%;
    height: 100%;
  }
  .item {
    position: relative;
    width: 100rem;
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
        animation: movebg 60s infinite alternate;
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
      background-position: 50% 50%;
    }
    100% {
      background-position: 0% 50%;
    }
 } 
  
</style>