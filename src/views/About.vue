<template>
  <div class="about">
    <div class="bg">
      <div class="backVideo">
        <video
          src="../assets/video/bg_1_blur.mp4"
          loop="loop"
          muted="muted"
          autoplay="true"
        ></video>
      </div>
      <div class="middleWrap">
        <video
          src="../assets/video/bg_1.mp4"
          loop="loop"
          muted="muted"
          autoplay="true"
        ></video>
      </div>
      <div class="frontWrap">
        <div class="mask">
          <video
            src="../assets/video/bg_1.mp4"
            loop="loop"
            muted="muted"
            autoplay="true"
          ></video>
        </div>
      </div>
    </div>
    <div class="main">
      <svg
        viewBox="0 0 253.5 451"
        class="bottle"
        style="opacity: 1; visibility: inherit"
      >
        <g data-v-a1d7bf90="" id="Group_22_1_" transform="translate(0.5 0.5)">
          <path
            d="M128.9,128.2c0,0,1.4,127.3-1.7,160.1c-4,42.5-29.5,100.4-46,117.9l-4.8-2c16.6-17.5,40.8-73.4,44.8-115.9c3.1-32.8,1.7-160.1,1.7-160.1"
            class="st0"
            style="strokeDashoffset: 0; strokeDasharray: none"
          ></path>
          <path
            d="M134.4,123.3v4.9h-16.2v-4.9"
            class="st0"
            style="stroke-dashoffset: 0; stroke-dasharray: none"
          ></path>
          <path
            d="M98.8,0h54.9c11,0,20,9,20,20v100.6l0,0H78.8l0,0V20C78.8,9,87.7,0,98.8,0z"
            class="st0"
            style="stroke-dashoffset: 0; stroke-dasharray: none"
          ></path>
          <rect
            x="83.9"
            y="120.6"
            width="84.7"
            height="2.7"
            class="st0"
            style="stroke-dashoffset: 0; stroke-dasharray: none"
          ></rect>
          <path
            d="M83.9,123.3c-6.2,0-16.8,2.6-19.9,11.9s-7.5,18.1-17.7,23.8C36.2,164.8,0,194.4,0,252.6V424c0,6.6,0,26,16.8,26h218.9c16.8,0,16.8-19.4,16.8-26V252.6c0-58.3-36.2-87.9-46.4-93.6s-14.6-14.6-17.7-23.8s-13.7-11.9-19.9-11.9L83.9,123.3z"
            class="st0"
            style="stroke-dashoffset: 0; stroke-dasharray: none"
          ></path>
          <path
            d="M87.2,128.2c-12.6,0-15.5,10.4-18.3,19c-2.8,8.5-6.9,16.7-16.3,22c-9.3,5.3-42.7,32.5-42.7,86.2v150.8c0,6.1,0,24,15.5,24c41,0,27.7-24.8,101.1-24.8s68.5,24.8,100.6,24.8c15.5,0,15.5-17.9,15.5-24V255.3c0-53.7-33.3-80.9-42.7-86.2s-13.4-13.4-16.3-22s-4.5-19-18.3-19H87.2z"
            class="st0"
            style="stroke-dashoffset: 0; stroke-dasharray: none"
          ></path>
        </g>
      </svg>
    </div>
  </div>
</template>

<script>
export default {
  name: "About",
};
</script>

<style lang="scss" scoped>
.about {
  position: relative;
  width: 100%;
  height: 100%;
}
.bg {
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
  .backVideo {
    position: absolute;
    top: -100px;
    right: 0px;
    width: 100%;
    height: 100%;
    z-index: 1;
  }
  .middleWrap {
    position: absolute;
    top: -100px;
    right: 0px;
    width: 100%;
    height: 100%;
    z-index: 2;
    //opacity: 0;
    animation: opacity1 2s;
  }
  .frontWrap {
    position: absolute;
    top: -100px;
    right: 0px;
    width: 100%;
    height: 100%;
    z-index: 3;
    .mask {
      -webkit-mask: url("../assets/img/bottle.svg") no-repeat;
      mask-position: 10vw 50%;
      mask-size: auto 80vh;
    }
    
  }
}
.main {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 5;
  .bottle {
    position: absolute;
    top: 10%;
    left: 10%;
    height: 80%;
    .st0 {
      fill: none;
      stroke: #fff;
      stroke-width: 1;
      animation: changeOffset 5s ease;
    }
  }
}

//实现线条流动效果
@keyframes changeOffset {
  0% {
    stroke-dashoffset: -800;
    stroke-dasharray:400,600;
  }
  100% {
    stroke-dashoffset: 0;
  }
}

//消失效果
@keyframes opacity1 {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}
</style>
