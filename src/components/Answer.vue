<template>
    <label :for="id" :class="classes">
        <input :id="id" name="answer" type="radio" :disabled="disabled" :value="value" v-model="model"/>
        {{ value }}
    </label>
</template>
<script setup>
import { computed } from 'vue';

const props = defineProps({
    id:String,
    value:String,
    disabled:Boolean,
    correctAnswer:String
})
const model= defineModel();
const classes = computed(()=>({
   right:props.disabled && props.value === props.correctAnswer,
   wrong:props.disabled && props.value !== props.correctAnswer
}))
</script>

<style>
.right{
    color: green;
}

.wrong{
    color: red;
}

</style>