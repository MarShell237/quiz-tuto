<template>
  <h1>Recapitulatif</h1>
  <Success v-if="hasWon" :message="quiz.success_message"/>
  <Failled v-else :message="quiz.failure_message"/>
  <Score :score="score +'/'+ quiz.questions.length"/>
</template>
  
<script setup>
import {  computed } from 'vue';
import Score from './Score.vue';
import Success from './Success.vue';
import Failled from './Failled.vue';
const props = defineProps({
    quiz:Object,
    answers: Array
  })

  const score = computed(()=>{
    return props.quiz.questions.reduce((acc,question,cle) => {
      if (props.answers[cle] === question.correct_answer) {
        return acc+1
      }
      return acc
    },0)
  })

  const hasWon = computed(()=>{
    return score.value >= props.quiz.minimum_score    
  })
</script>

<style scoped>
  
</style>