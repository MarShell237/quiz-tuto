<template>
  <div>
    <div class="question">
      <h3>{{ question.question }}</h3>
        <div v-for="(choice,index) in randonChoises" :key="choice">
          <Answer :id="`answer${index}`"
                  :disabled="answer"
                  :value="choice"
                  v-model="answer"
                  :correctAnswer="question.correct_answer"
          />
        </div>
      <button :disabled="!answer" @click="emits('answer',answer)">question suivante</button>
    </div>
  </div>
</template>

<script setup>
  import { shuffleArray } from '@/composable/array';
  import { ref, computed} from 'vue';
  import Answer from './Answer.vue';
  const props = defineProps({
    question:Object
  })

  const emits = defineEmits(['answer'])

  const answer = ref(null)
  
  const randonChoises = computed(()=> shuffleArray(props.question.choices))
</script>

<style scoped>
  .question{
    padding-top: 2rem;
  }

  li{
    list-style-type: none;
  }
</style>