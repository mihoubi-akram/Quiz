<template>
    Recap
    <p>
        {{hasWon ? quiz.success_message:quiz.failure_message}}
    </p>
    <p>
        Score : {{ score }} / {{ quiz.questions.length }}
    </p>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
    answers:Array,
    quiz:Object
})
const score = computed(()=>{
    let score = 0;
    props.quiz.questions.forEach((question,index) => {
        if(question['correct_answer'] == props.answers[index]){
            score++;
        }
    });
    return score;
})
const hasWon = computed(()=> score.value > props.quiz.minimum_score);
</script>