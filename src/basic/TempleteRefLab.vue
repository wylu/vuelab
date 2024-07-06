<template>
  <input ref="input" />

  <!-- v-for 中的模板引用 -->
  <p></p>
  <ul>
    <li v-for="item in list" :key="item" ref="itemRefs">
      {{ item }}
    </li>
  </ul>

  <!-- 函数模板引用 -->
  <p></p>
  <input
    :ref="
      (el) => {
        console.log(`function template ref: ${el}`)
      }
    "
  />

  <!-- 组件上的 ref -->
  <p></p>
  <HelloWorld msg="You did it!" ref="child"></HelloWorld>
</template>

<script setup lang="ts">
import { ref, onMounted, watchEffect } from 'vue'
import HelloWorld from '../components/HelloWorld.vue'

// 声明一个 ref 来存放该元素的引用
// 必须和模板里的 ref 同名
const input = ref<HTMLInputElement | null>(null)

onMounted(() => {
  console.log('input onMounted')
  input.value?.focus()
})

watchEffect(() => {
  if (input.value) {
    console.log(`input value: ${input.value}`)
  } else {
    // 此时还未挂载，或此元素已经被卸载（例如通过 v-if 控制）
    console.log(`input value: ${input.value}`)
  }
})

const list = ref(['Alice', 'Bob', 'Charlie'])
const itemRefs = ref([])

onMounted(() => console.log(itemRefs.value))

const child = ref(null)

onMounted(() => {
  // child.value 是 <HelloWorld /> 组件的实例
  console.log(`HelloWorld onMounted: ${child.value}`)
})
</script>
