<template>
  <!-- v-for -->
  <li :key="index" v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
  <li :key="i" v-for="(item, i) in items">
    {{ parentMessage }} - {{ i }}
    <span :key="j" v-for="(friend, j) in item.friends"> - {{ friend }}</span>
  </li>

  <!-- v-for 与对象 -->
  <ul>
    <li :key="index" v-for="(value, key, index) in myObject">
      {{ index }}. {{ key }}: {{ value }}
    </li>
  </ul>

  <!-- 在 v-for 里使用范围值 -->
  <p>
    <span :key="i" v-for="i in 10">{{ i }}</span>
  </p>

  <!-- <template> 上的 v-for -->
  <ul>
    <template v-for="item in items" :key="item.message">
      <li>{{ item.message }}</li>
      <li>friends: {{ item.friends }}</li>
    </template>
  </ul>

  <!-- v-for 与 v-if -->
  <template v-for="todo in todos">
    <li v-if="!todo.isComplete" :key="todo.name">
      {{ todo.name }}
    </li>
  </template>
</template>

<script setup lang="ts">
import { reactive, ref } from 'vue'

const parentMessage = ref('Parent')
const items = ref([
  { message: 'Foo', friends: ['Alice', 'Bob'] },
  { message: 'Bar', friends: ['Carol', 'Charlie', 'Dave'] }
])

const myObject = reactive({
  title: 'How to do lists in Vue',
  author: 'Jane Doe',
  publishedAt: '2016-04-10'
})

const todos = reactive([
  { name: 'Foo', isComplete: true },
  { name: 'Bar', isComplete: false }
])
</script>
