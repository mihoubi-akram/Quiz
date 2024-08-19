<template>
    <label :for="id">
        <input :disabled="disabled" type="radio" name="answer" :id="id" :value="value" v-model="model"/>
        {{ value }}
    </label>
</template>
<script setup>
const props = defineProps({
    id:String,
    value:String,
    disabled:Boolean,
    correctAnswer:String
})
const model= defineModel();
</script>