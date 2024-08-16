<template>
  <header>
    <div class="container">
      <div v-if="state === 'error'"> 
        <p>
          Impossible de charger le quiz
        </p>
      </div>
      <div :aria-busy="state === 'loading'">
        <Quiz :quiz="quiz" v-if="quiz"/>
      </div>

    </div>
  </header>

</template>
<script setup>
import Quiz from './components/Quiz.vue'
import { onMounted, ref } from 'vue';
const quiz = ref(null);
const state = ref('loading');

onMounted(()=>{
   fetch('/data.json')
    .then(r=>{
      if(r.ok){
        return r.json();
      }
      throw new Error('Impossible de recupérer le json')
    })
    .then(data=>{
      quiz.value = data
      state.value = 'idle'
    })
    .catch(e=>{
      state.value = "error"
    })
})
</script>


<style scoped>
.container {
  width: 80%;
  max-width: 1200px;
  margin: 0 auto;   
  padding: 20px; 
  background-color: #f9f9f9; 
  border: 1px solid #ddd; 
  border-radius: 8px; 
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); 
}
</style>
