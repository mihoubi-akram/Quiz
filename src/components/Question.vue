<template>
  <div class="question">
    <p> {{ question.question }}</p>
    <ul>
      <li v-for="(choice, index) in randomChoices" :key="choice" >
        <Answer :id="`choice-${index}`" :value="choice" :disabled="hasAnswer" :correctAnswer="question.correct_answer" v-model="answer"></Answer>
      </li>
    </ul>
    <button :disabled="!hasAnswer" @click="emits('answer',answer)"> Suivant</button>
  </div>
</template>

<script setup>
import Answer from './Answer.vue';
import { shuffle } from '@/functions/array';
import { computed, ref } from 'vue';
const props = defineProps({
    question:Object
})

const emits = defineEmits(['answer']);
const hasAnswer = computed(()=>answer.value !== null);
const answer = ref(null);
const randomChoices = computed(()=>shuffle(props.question.choices));
</script>

<style>

.question{
    padding: 5px;
}
.question button{
    display: block;
    margin-left: auto;
}
.question li {  
  list-style-type: none;  
}
</style>