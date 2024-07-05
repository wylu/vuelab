<template>
    <button @click="awesome = !awesome">Toggle</button>

    <h1 v-if="awesome">Vue is awesome!</h1>
    <h1 v-else>Oh no 😢</h1>

    <div v-if="type === 'A'">A</div>
    <div v-else-if="type === 'B'">B</div>
    <div v-else-if="type === 'C'">C</div>
    <div v-else>Not A/B/C</div>

    <button @click="ok = !ok">Toggle</button>
    <h1 v-show="ok">Hello!</h1>
</template>

<script setup lang="ts">
import { ref } from "vue";

const awesome = ref(true)
const ok = ref(true)
</script>