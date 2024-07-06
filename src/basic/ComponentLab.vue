<template>
  <h2>Here are some child components!</h2>
  <ButtonCounter />
  <p></p>
  <ButtonCounter />
  <p></p>
  <ButtonCounter />

  <!-- 传递 props -->
  <!-- 监听事件 -->
  <p></p>
  <div :style="{ fontSize: postFontSize + 'em' }">
    <BlogPost
      v-for="post in posts"
      :key="post.id"
      :title="post.title"
      @enlarge-text="postFontSize += 0.1"
    />
  </div>

  <!-- 通过插槽来分配内容 -->
  <p></p>
  <AlertBox>Something bad happened.</AlertBox>

  <!-- 动态组件 -->
  <p></p>
  <div class="demo">
    <button
      v-for="(_, tab) in tabs"
      :key="tab"
      :class="['tab-button', { active: currentTab === tab }]"
      @click="currentTab = tab"
    >
      {{ tab }}
    </button>
    <component :is="tabs[currentTab]" class="tab"></component>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

import ButtonCounter from '../components/ButtonCounter.vue'
import BlogPost from '../components/BlogPost.vue'
import AlertBox from '../components/AlertBox.vue'

const posts = ref([
  { id: 1, title: 'My journet with Vue' },
  { id: 2, title: 'Blogging with Vue' },
  { id: 3, title: 'Why Vue is so fun' }
])

const postFontSize = ref(1)

import HomePage from '../components/HomePage.vue'
import PostPage from '../components/PostPage.vue'
import ArchivePage from '../components/ArchivePage.vue'

const currentTab = ref('home')
const tabs = {
  home: HomePage,
  post: PostPage,
  archive: ArchivePage
}
// const tabs = {
//   HomePage,
//   PostPage,
//   ArchivePage
// }
console.log(`tabs: ${JSON.stringify(tabs)}`)
</script>

<style>
.demo {
  font-family: sans-serif;
  border: 1px solid #eee;
  border-radius: 2px;
  padding: 20px 30px;
  margin-top: 1em;
  margin-bottom: 40px;
  user-select: none;
  overflow-x: auto;
}

.tab-button {
  padding: 6px 10px;
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
  border: 1px solid #ccc;
  cursor: pointer;
  background: #f0f0f0;
  margin-bottom: -1px;
  margin-right: -1px;
}
.tab-button:hover {
  background: #e0e0e0;
}
.tab-button.active {
  background: #e0e0e0;
}
.tab {
  border: 1px solid #ccc;
  padding: 10px;
}
</style>
