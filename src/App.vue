<template>
  <div class="container">
    <p v-if="state === 'error'">
      Impossible de charger le quiz
    </p>
    <div :aria-busy="state === 'loading'">
      <Quiz :quiz="quiz" v-if="quiz"/>
    </div>
  </div>
</template>

<script setup>
  import {ref,onMounted} from 'vue'
  import Quiz from './components/Quiz.vue'
  const quiz = ref(null);
  const state = ref('loading')

onMounted(()=>{
  fetch('./public/informatique.json')
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
  .catch(err => {
    state.value = 'error'
  })
})
</script>

<style scoped>
  .container{
    margin-top: 2rem;
  }
</style>
