<template>
    <label :for="id" :class="classes">
        <input :disabled="disabled" :id="id" :value="value" type="radio"  name="answer" v-model="model" >
        {{ value }}
    </label>
</template>

<script setup>
import { computed } from 'vue'
const props = defineProps({
    id:String,
    disabled:Boolean,
    value:String,
    correct_answer:String
})

const model = defineModel()

const classes = computed(()=>({
    disabled: props.disabled,
    correct: props.disabled && props.value === props.correct_answer,
    wrong: props.disabled && props.value !== props.correct_answer && model.value === props.value
}))
</script>

<style>
.disabled{opacity: .5;}
.correct{
    opacity: 1;
    color: green;
}
.wrong{
    opacity: 1;
    color: red;
}
</style>