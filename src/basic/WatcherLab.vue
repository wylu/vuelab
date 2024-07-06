<template>
  <!-- 侦听器 -->
  <p>
    Ask a yes/no question:
    <input v-model="question" :disabled="loading" />
  </p>
  <p>{{ answer }}</p>

  <!-- 侦听数据源类型 -->
  <p></p>
  <span>{{ x }}+</span>
  <span>{{ y }}=</span>
  <span>{{ z }}</span>
  <p></p>
  <button @click="x++">Add x</button>
  <button @click="x--">Sub x</button>
  <p></p>
  <button @click="y++">Add y</button>
  <button @click="y--">Sub y</button>

  <!-- 深层侦听器 -->
  <p></p>
  <div>{{ obj.count }}</div>
  <button @click="obj.count++">Add count</button>

  <p></p>
  <div>{{ state.someObject.count }}</div>
  <button @click="state.someObject.count++">Add count</button>
  <button @click="state.someObject = { count: 0 }">Reset count</button>

  <!-- 即时回调的侦听器 -->
  <p></p>
  <div>{{ source.count }}</div>
  <button @click="source.count++">Add count</button>

  <!-- 一次性侦听器 -->
  <p></p>
  <div>IPv6: {{ ipv6.enable }}</div>
  <button @click="ipv6.enable = !ipv6.enable" :disabled="ipv6.enable">Enable IPv6</button>

  <!-- watchEffect() -->
  <p></p>
  <div>todoId: {{ todoId }}</div>
  <div>data: {{ data }}</div>
  <button @click="todoId++">Add todoId</button>
</template>

<script setup lang="ts">
import { ref, computed, watch, reactive, watchEffect } from 'vue'

const question = ref('')
const answer = ref('Questions usually contain a question mark. ;-)')
const loading = ref(false)

// 可以直接监听一个 ref
watch(question, async (newQuestion, oldQuestion) => {
  console.log('old question: ', oldQuestion)
  console.log('new question: ', newQuestion)
  if (newQuestion.includes('?')) {
    loading.value = true
    answer.value = 'Thinking...'
    try {
      const res = await fetch('https://yesno.wtf/api')
      answer.value = (await res.json()).answer
    } catch (error) {
      answer.value = 'Error! Could not read the API.' + error
    } finally {
      loading.value = false
    }
  }
})

const x = ref(0)
const y = ref(0)
const z = computed(() => {
  return x.value + y.value
})

// 单个 ref
watch(x, (newX) => {
  console.log(`x is ${newX}`)
})

// getter 函数
watch(
  () => x.value + y.value,
  (sum) => {
    console.log(`sum of x + y is: ${sum}`)
  }
)

// 多个来源组成的数组
watch([x, () => y.value], ([newX, newY]) => {
  console.log(`x is ${newX} and y is ${newY}`)
})

const obj = reactive({ count: 0 })

watch(obj, (newValue, oldValue) => {
  // 在嵌套的属性变更时触发
  // 注意：`newValue` 此处和 `oldValue` 是相等的
  // 因为它们是同一个对象！
  console.log(`oldValue: ${JSON.stringify(oldValue)}`)
  console.log(`newValue: ${JSON.stringify(newValue)}`)
  console.log(`Object.is(newValue, oldValue): ${Object.is(newValue, oldValue)}`)
})

const state = reactive({
  someObject: {
    count: 0
  }
})

watch(
  () => state.someObject,
  () => {
    // 仅当 state.someObject 被替换时触发
    console.log(`someObject replaced: ${JSON.stringify(state.someObject)}`)
  },
  { deep: true }
)

const source = reactive({ count: 0 })

watch(
  source,
  (newValue, oldValue) => {
    // 立即执行，且当 `source` 改变时再次执行
    console.log(`oldValue: ${JSON.stringify(oldValue)}, newValue: ${JSON.stringify(newValue)}`)
  },
  { immediate: true }
)

const ipv6 = reactive({ enable: false })

watch(
  ipv6,
  () => {
    console.log('enable ipv6')
  },
  { once: true }
)

const todoId = ref(1)
const data = ref(null)

// watch(
//   todoId,
//   async () => {
//     const response = await fetch(`https://jsonplaceholder.typicode.com/todos/${todoId.value}`)
//     data.value = await response.json()
//   },
//   { immediate: true }
// )

watchEffect(async () => {
  const response = await fetch(`https://jsonplaceholder.typicode.com/todos/${todoId.value}`)
  data.value = await response.json()
})
</script>
