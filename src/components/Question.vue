<template>
  <div class="question">
    <p> {{ question.question }}</p>
    <ul>
      <li v-for="(choice, index) in randomChoices" :key="choice" >
        <label :for="`choice-${index}`">
          <input :disabled="hasAnswer" type="radio" name="answer" :id="`choice-${index}`" :value="choice" v-model="answer"/>
          {{ choice }}
        </label>
      </li>
    </ul>
    <button :disabled="!hasAnswer" @click="emits('answer',answer)"> Suivant</button>
  </div>
</template>

<script setup>
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