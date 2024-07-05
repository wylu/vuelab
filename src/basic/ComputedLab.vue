<template>
  <p>Has published books:</p>
  <span>{{ publishedBooksMessage }}</span>
  <p><button @click="clearBooks">Clear Books</button></p>

  <p>{{ fullName }}</p>
  <p>{{ firstName }} {{ lastName }}</p>
  <p><button @click="changeName">Change Name</button></p>
</template>

<script setup lang="ts">
import { ref, reactive, computed } from 'vue'

const author = reactive({
  name: 'John Doe',
  books: ['Vue 2 - Advanced Guide', 'Vue 3 - Basic Guide', 'Vue 4 - The Mystery']
})

const publishedBooksMessage = computed(() => {
  return author.books.length > 0 ? 'Yes' : 'No'
})

const clearBooks = () => {
  author.books = []
}

const firstName = ref('John')
const lastName = ref('Doe')

const fullName = computed({
  // getter
  get() {
    return firstName.value + ' ' + lastName.value
  },
  // setter
  set(newValue) {
    ;[firstName.value, lastName.value] = newValue.split(' ')
  }
})

function changeName() {
  fullName.value = 'Warren Buffett'
}
</script>
