<template>
    <span> Etape {{step+1}} / {{maxStep+1}}</span>
    <progress :value="step" :max="maxStep" />
</template>

<script setup>
defineProps({
  maxStep:Number,
  step:Number
})
</script>