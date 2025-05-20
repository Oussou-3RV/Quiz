<template>
    <div class="question">
        <h3>{{ question.question }}</h3>
        <ul>
            <li v-for="(choice,index) in RandomTable" :key="choice" >
                <Answer :id="`answer${index}`"
                 :disabled="hasAnswer"
                 :value="choice"
                  v-model="answer"
                  :correct_answer="question.correct_answer"/>
            </li>
        </ul>
        <button :disabled="!hasAnswer" @click="emits('answerr',answer)">Question suivante</button>
        
    </div>
</template>

<script setup>
import { shuffleArray } from '@/functions/Arrays';
import { computed, ref } from 'vue';
import Answer from './Answer.vue';


const props = defineProps({
    question:Object
})

const answer = ref(null)
const hasAnswer = computed(() => answer.value != null)
//crée un évènement qui detecte qd une réponse est séléctionnée et active le btn Question suivante
const emits = defineEmits(['answerr'])

const RandomTable = computed(() => shuffleArray(props.question.choices)) 


</script>
<style>
.question{
    padding-top: 2rem;
}
li{
    list-style: none;
}
.question button{
    display: block;
    margin-left: auto;
}
</style>