<template>
  <div>
    <h1>{{ quiz.title  }}</h1>
    <Progress :value="step" 
              :max="quiz.questions.length - 1"
    />

    <Question :key="question.question" 
              :question="question" 
              @answer="addAnswer" 
              v-if="state === 'question'"
    />

    <Recap :answers="answers"
          :quiz="quiz" 
          v-if="state === 'recap'"
    />
  </div>
</template>

<script setup>
import Progress from './Progress.vue';
import Question from './Question.vue';
import { ref, computed } from 'vue';
import Recap from './Recap.vue';
  const props = defineProps({
    quiz:Object
  })
  const state = ref('question')
  const answers = ref(props.quiz.questions.map(()=>null))
  const step = ref(0)
  const question = computed(()=>props.quiz.questions[step.value])

  function addAnswer(answer){
    answers.value[step.value] = answer;
    if(step.value === props.quiz.questions.length - 1){
      state.value = 'recap';
    }else{
      step.value++
    }

  }
</script>

<style scoped>

</style>