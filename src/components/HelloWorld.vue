<script setup lang="ts">
import { ref, reactive } from 'vue'
import a from '../../static/imgs/a.png'
import b from '../../static/imgs/b.png'
import c from '../../static/imgs/c.png'
import d from '../../static/imgs/d.png'
defineProps<{ msg: string }>()

const duration = '1s'   // 轮播间隔
const state = 'paused' // hover时暂停与否(默认：running)  'paused' || 'running'

let count = ref(0)
let imgs = reactive([a,b,c,d])

function ani() {
  count.value += 1
  if(count.value > imgs.length - 1) {
    count.value = 0
  }
}
</script>

<template>
  <h1>{{ msg }}</h1>
  <div class="imgs" @animationiteration="ani">
    <div class="box">
      <img class="item" v-for="(d,i) in imgs" :key="i" :src="d" alt="">
    </div>
  </div>
</template>

<style scoped>
.imgs {
  position: relative;
  width: 800px;
  height: 400px;
  counter-reset: num 0;
  animation: scroll v-bind(duration) infinite;
  overflow: hidden;
}
.imgs:hover {
  animation-play-state: v-bind(state);
}
@keyframes scroll {
  to {}
}
.box {
  display: flex;
  height: 100%;
  transform: translateX(calc(-100% * v-bind(count)));
  transition: 0.3s;
}
.item {
  width: 100%;
  height: 100%;
  flex-shrink: 0;
}
</style>
