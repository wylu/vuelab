<template>
  <li>
    {{ title }}
    <button @click="$emit('remove')">Remove</button>
  </li>
</template>

<script setup lang="ts">
defineProps(['title'])
defineEmits(['remove'])
</script>
