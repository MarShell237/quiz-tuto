<template>
  <div>
    <h1>{{ quiz.title  }}</h1>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
  defineProps({quiz:Object})
  const step = ref(0)
</script>

<style scoped>

</style>