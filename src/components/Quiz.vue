<template>
   <div>
    <h1>{{ quizGeneral.title }}</h1>
    <Progress :valeur="stepInitial" :max="quizGeneral.questions.length-1"/>
    <Question :question="currentQuestion" :key="currentQuestion.question" v-if="state === 'modeQuestion'" @answerr="addAnswer" />
    <Recap v-if="state =='modeRecap'" :answers="answers" :quizG="quizGeneral"/> 
   
    
   </div>
</template>

<script setup>
import { computed, ref } from 'vue';
import Progress from './Progress.vue';
import Question from './Question.vue';
import Recap from './Recap.vue';

const stepInitial = ref(0)
const state = ref('modeQuestion')
const props = defineProps({
    quizGeneral:Object
})
const answers = ref(props.quizGeneral.questions.map(()=> null))

//va representer chaque question de la liste une a une
const currentQuestion = computed(()=>{
    return props.quizGeneral.questions[stepInitial.value]
})

const addAnswer = (answer) =>{
    
    answers.value[stepInitial.value] = answer ;
    //Si l'incrementation atteint la taille tu tableau : state = recapitulatif
    if(stepInitial.value == answers.value.length-1)
        state.value = 'modeRecap'
    else
        stepInitial.value++;

    
}
</script>