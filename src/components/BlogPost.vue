<template>
  <h4>{{ title }}</h4>
  <button @click="$emit('enlarge-text')">Enlarge text</button>
</template>

<script setup lang="ts">
defineProps(['title'])
</script>
