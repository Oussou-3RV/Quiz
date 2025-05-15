<template>
    <div class="question">
        <h3>{{ question.question }}</h3>
        <ul>
            <li v-for="(choice,index) in question.choices" :key="choice">
                <label :for="`answer${index}`">
                    <input type="radio" :id="`answer${index}`" name="answer" v-model="answer" :value="choice">
                    {{ choice }}
                </label>
            </li>
        </ul>
        <button :disabled="!hasAnswer" @click="emits('answerr',answer)">Question suivante</button>
        
    </div>
</template>

<script setup>
import { computed, ref } from 'vue';

defineProps({
    question:Object
})

const answer = ref(null)
const hasAnswer = computed(() => answer.value != null)
//crée un évènement qui detecte qd une réponse est séléctionnée
const emits = defineEmits(['answerr'])


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