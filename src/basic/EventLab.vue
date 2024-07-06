<template>
  <!-- 内联事件处理器 -->
  <button @click="count++">Add 1</button>
  <p>Count is: {{ count }}</p>

  <!-- 方法事件处理器 -->
  <button @click="greet">Greet</button>

  <!-- 在内联处理器中调用方法 -->
  <p>
    <button @click="say('hello')">Say hello</button>
  </p>
  <p>
    <button @click="say('bye')">Say bye</button>
  </p>

  <!-- 在内联事件处理器中访问事件参数 -->
  <p>
    <!-- 使用特殊的 $event 变量 -->
    <button @click="warn('Form cannot be submitted yet.', $event)">Submit</button>
  </p>
  <p>
    <!-- 使用内联箭头函数 -->
    <button @click="(event) => warn('Form cannot be submitted yet.', event)">Submit</button>
  </p>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const count = ref(0)

const name = ref('Vue.js')

function greet(event: Event) {
  alert(`Hello ${name.value}!`)
  // `event` 是 DOM 原生事件
  if (event) {
    alert((event.target as HTMLButtonElement).tagName)
  }
}

function say(message: string) {
  alert(message)
}

function warn(message: string, event: Event) {
  // 这里可以访问原生事件
  if (event) {
    event.preventDefault()
  }
  alert(message)
}
</script>
