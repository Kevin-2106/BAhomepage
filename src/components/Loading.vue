<script setup>
import { ref } from 'vue'

const prop = defineProps(['percent'])

const imgUrl = ref('https://webcnstatic.yostar.net/ba_cn_web/prod/web/assets/avatar2.b84283e9.png')
const imgList = [
  'https://webcnstatic.yostar.net/ba_cn_web/prod/web/assets/avatar1.c18ce793.png',
  'https://webcnstatic.yostar.net/ba_cn_web/prod/web/assets/avatar2.b84283e9.png',
  'https://webcnstatic.yostar.net/ba_cn_web/prod/web/assets/avatar3.c9d108f1.png',
  'https://webcnstatic.yostar.net/ba_cn_web/prod/web/assets/avatar4.8656c817.png'
]

document.oncontextmenu = function () {
  return false
}
const options = {
  // 动画时长
  duration: 2000,
  // 动画前后保持的状态
  fill: 'forwards',
  // 动画缓动类型
  easing: 'ease-in-out'
}
let a = 0
imgUrl.value = imgList[a % 4]
a++
setInterval(() => {
  imgUrl.value = imgList[a % 4]
  a++
}, 2000)
</script>

<script>
export default {
  data() {
    return {
      randomTips: ['首次加载可能较慢，请耐心等待……', 'Blue Archive真的是一款积极向上的游戏！', '色色的事情不行！死刑！', '音频只有点击页面任意位置后才能播放！', 'B站关注Kevin_2106谢谢喵', 'BA启动！', '就不暴击 蒸馍，你不扶器？'],
      tipIndex: 0
    }
  },
  mounted() {
    setInterval(() => {
      this.tipIndex = Math.floor(Math.random() * this.randomTips.length)
    }, 1000)
  }
}
</script>

<template>
  <div class="loading_wrapper">
    <div ref="loadingImg" class="avatar_img bounce-top">
      <img class="loading" :src="imgUrl" alt="" />
      <div class="hide">
        <img :src="imgList[0]" alt="" />
        <img :src="imgList[1]" alt="" />
        <img :src="imgList[2]" alt="" />
        <img :src="imgList[3]" alt="" />
        <img src="/shitim/Tran_Shitim_Icon.png" alt="" />
      </div>
    </div>
    <div class="progress_wrapper">
      <h1 class="title">connecting...</h1>
      <div class="percent">{{ Math.floor(prop.percent * 100) + '%' }}</div>
      <div class="tip">{{ randomTips[tipIndex] }}</div>
    </div>
  </div>
</template>




<style scoped>
@keyframes move {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-1.6666666667rem);
  }
  100% {
    transform: translateY(0);
  }
}

.loading {
  animation: move 2s ease-in-out infinite;
}

img {
  user-select: none;
  -webkit-user-drag: none;
}

@font-face {
  font-family: TVPS-Vain-Capital-2;
  src: url(https://webcnstatic.yostar.net/ba_cn_web/prod/web/assets/TVPS-Vain-Capital-2.cca90a05.ttf);
}

.loading_wrapper {
  background: url('https://webcnstatic.yostar.net/ba_cn_web/prod/web/assets/loading_bg_pc.ba246778.png')
    center;
  background-size: cover;
  overflow: hidden;
  z-index: 99;
}

.loading_wrapper {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.progress_wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.progress_wrapper .title {
  font-family: TVPS-Vain-Capital-2, system-ui;
  color: #1289f9;
  font-size: 1.8rem;
}

.progress_wrapper .percent {
  margin-top: 0.3666666667rem;
  font-size: 1.4rem;
  font-family: TVPS-Vain-Capital-2, system-ui;
  color: #1289f9;
}

.progress_wrapper .tip {
  margin-top: 1rem;
  font-size: 1.0rem;
  font-family: TVPS-Vain-Capital-2, system-ui;
  color: #1289f9;
}

.hide {
  opacity: 0;
  position: absolute;
  z-index: -1;
  top: 0;
  left: 0;
}

.avatar_img {
  height: 340px;
}
</style>
