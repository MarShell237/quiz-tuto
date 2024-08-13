<template>
  <div>     
    {{ quiz }}  
  </div>
</template>

<script setup>
  import {ref,onMounted} from 'vue'
  const quiz = ref(null);
  const state = ref('loading')

onMounted(()=>{
  fetch('./public/quiz.json')
  .then(response => {
    if(response.ok){
      return response.json()
      
    }
    throw new Error('impossible de recuperer le json')
  })    
  .then(data => {
    quiz.value = data;
    state.value = 'idle'
  })
})
</script>

<style scoped>

</style>
