<template>
    <div v-if="displayMode=='question'">
        <h4>{{ quiz.title }}</h4>
        <ProgressBar :step="step" :maxStep="quiz.questions.length-1"></ProgressBar>
        <Question :key="question.question" :question="question" @answer="handleAnswer"></Question>
    </div>
    <div v-else>
      <Recap :answers ="answers" :quiz="quiz"></Recap>
    </div>
    
</template>
<script setup>
// 
import { computed, ref,defineEmits } from 'vue';
import ProgressBar from './ProgressBar.vue';
import Question from './Question.vue';
import Recap from './Recap.vue';
const props = defineProps({
  quiz:Object,
})

const step = ref(0);
const question = computed(()=>props.quiz.questions[step.value]);

const answers = ref (Array(props.quiz.questions.length));
const nbquestion = computed(()=>props.quiz.questions.length);
const displayMode  = ref("question");
const handleAnswer =(answer)=>{
  answers.value[step.value] = answer;
  if(step.value === nbquestion.value-1 ){
    displayMode.value = 'recap';
  }else{
    step.value++;
  }
}
</script>

<style>


</style>
