<script setup>
import { ref } from 'vue'
import config from '/_config.json'

const curtain = ref(false)

const skip = () => {
  curtain.value = true
  setTimeout(() => {
    window.open(config.task.href)
  }, 1000)
  setTimeout(
    () => {
      curtain.value = false
    },
    Math.floor(Math.random() * 4 + 2) * 500
  )
}
</script>

<template>
  <div :name="config.task.name" class="task css-cursor-hover-enabled" @click="skip"></div>
  <transition name="curtain">
    <div v-if="curtain" class="curtain">
      <img src="/shitim/Tran_Shitim_Icon.png" alt="" />
    </div>
  </transition>
</template>

<style scoped>
.curtain {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: url('/shitim/Event_Main_Stage_Bg.png') center;
  background-size: cover;
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.curtain img {
  width: 500px;
  height: auto;
}

.task {
  position: absolute;
  bottom: 140px;
  right: 60px;
  width: 150px;
  height: 150px;
  background: url('/task.png') center;
  background-size: cover;
  transition: transform 0.1s;
}

.task:before {
  content: '';
  position: absolute;
  left: 10px;
  bottom: 0;
  height: 50px;
  width: calc(100% + 10px);
  border-radius: 8px;
  background: #003153;
  transform: skewX(-10deg);
}

.task:after {
  content: attr(name);
  position: absolute;
  left: 10px;
  bottom: 0;
  height: 50px;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  font-size: 26px;
  font-weight: 800;
}

.task:active {
  transform: scale(0.9);
}

.curtain-enter-from {
  opacity: 0;
}

.curtain-enter-to {
  opacity: 1;
}

.curtain-leave-to {
  transform: scaleY(0%);
}

.curtain-leave-from {
  transform: scaleY(100%);
}

.curtain-leave-active,
.curtain-enter-active {
  transition:
    opacity 0.1s ease-in-out,
    transform 0.25s ease-in-out;
}

@media screen and (max-width: 495px) {
  .task {
    right: 40px;
  }
}
</style>
