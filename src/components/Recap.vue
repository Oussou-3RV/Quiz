<template>
    <h1>recap</h1>
    <p>
        Score : {{ score }} / {{quizG.questions.length}} 
    </p>
    <p>{{ hasWon ? quizG.success_message : quizG.failure_message }}</p>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
    quizG:Object,
    answers:Array
})

const score =  computed(() => {
    return props.quizG.questions.reduce((acc, question, k) => {
        if(question.correct_answer === props.answers[k])
            return acc+1
        else
            return acc
    },0)
})
const hasWon = computed(()=> score.value >= props.quizG.minimum_score )
</script>