<template>
  <label :for="id" :class="label_class">
    <input type="radio" 
            :id="id" 
            name="answer"
            :value="value"
            :disabled="disabled"
            :class="classes"
            v-model="model">
    {{ value }}
  </label>
</template>
  
<script setup>
import { computed }  from 'vue'
  const props = defineProps({
    id: String,
    disabled: String,
    value: String,
    correctAnswer: String
  })

  const model = defineModel()

  const classes = computed(()=>({
    right: props.disabled != null && props.value == props.correctAnswer,
    wrong: props.disabled != null && props.value !== props.correctAnswer
  }))
  
  const label_class = computed(()=>({
    disabled: props.disabled != null && model.value != props.value,
    right_label: props.disabled != null && props.value == props.correctAnswer,
    wrong_label: props.disabled != null && props.value !== props.correctAnswer
  }))  
</script>

<style scoped>
.disabled{
  opacity: .5;
}

.right{
  background-color: green;
}

.wrong{
  background-color: red;
}

.right_label{
  color: green;
}

.wrong_label{
  color: red;
}
</style>