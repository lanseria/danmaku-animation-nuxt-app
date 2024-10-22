<script setup lang="ts">
import { gsap } from 'gsap'

const danmakuAreaRef = useTemplateRef<HTMLDivElement>('danmakuAreaRef')
const messages = ref([
  'Hello!',
  'Cool!',
  'Awesome!',
  'Nice!',
  'Great!',
  'Wow!',
  'Amazing!',
  'Superb!',
  'Excellent',
  'Fantastic',
  'Brilliant',
  'Wonderful',
  'Terrific',
  'Fabulous',
  'Splendid',
  'Marvelous',
  'Incredible',
  'Spectacular',
  'Outstanding',
  'Phenomenal',
])

onMounted(() => {
  const danmakuMessages = danmakuAreaRef.value!.children

  gsap.set(danmakuMessages, {
    x: i => window.innerWidth + Math.random() * 100,
    y: () => Math.random() * danmakuAreaRef.value!.clientHeight,
    opacity: 0,
  })

  gsap.to(danmakuMessages, {
    duration: 10,
    x: -200,
    ease: 'none',
    stagger: {
      from: 'random',
      amount: 5,
    },
    repeat: -1,
    opacity: 1,
    onRepeat: () => {
      gsap.set(danmakuMessages, {
        x: i => window.innerWidth + Math.random() * 100,
        y: () => Math.random() * danmakuAreaRef.value!.clientHeight,
      })
    },
  })
})
</script>

<template>
  <div class="danmaku-container">
    <h1>Danmaku Animation</h1>
    <div ref="danmakuAreaRef" class="danmaku-area">
      <div v-for="(message, index) in messages" :key="index" class="danmaku-message">
        {{ message }}
      </div>
    </div>
  </div>
</template>

<style scoped>
.danmaku-container {
  font-family: Arial, sans-serif;
  text-align: center;
}

.danmaku-area {
  position: relative;
  width: 100%;
  height: 80vh;
  overflow: hidden;
  background-color: #f0f0f0;
}

.danmaku-message {
  position: absolute;
  font-size: 18px;
  color: #333;
  white-space: nowrap;
}
</style>
