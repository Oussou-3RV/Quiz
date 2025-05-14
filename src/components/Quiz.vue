<template>
   <div>
    <h1>{{ quizGeneral.title }}</h1>
    <Progress :valeur="stepInitial" :max="quizGeneral.questions.length-1"/>
    <Question :question="question"/>
   </div>
</template>

<script setup>
import { computed, ref } from 'vue';
import Progress from './Progress.vue';
import Question from './Question.vue';

const stepInitial = ref(2)

const props = defineProps({
    quizGeneral:Object
})

const question = computed(()=>{
    return props.quizGeneral.questions[stepInitial.value]
})
</script>