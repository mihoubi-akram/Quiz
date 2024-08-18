<template>
  <div class="question">
    <p> {{ question.question }}</p>
    <ul>
      <li v-for="(choice, index) in question.choices" :key="index" >
        
        <label :for="`choice-${index}`">
          <input type="radio" :id="`choice-${index}`" :value="choice"v-model="answer"/>
          {{ choice }}
        </label>
      </li>
    </ul>
    <button :disabled="!hasAnswer" @click="emit('answer',answer)"> Suivant</button>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue';
const props = defineProps({
    question:Object
})

const emit = defineEmits(['answer']);
const hasAnswer = computed(()=>answer.value !== null);
const answer = ref(null);
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