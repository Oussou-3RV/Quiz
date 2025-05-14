
<template>
 
 <div class="container">
  <div v-if="state === 'error'">
    <p> Impossible de charger le json ! </p>
  </div>

  <div :="state === 'loading'">
    <Quiz :quizGeneral="quiz" v-if="quiz!= null"/>
  </div>

 </div>


</template>

<script setup>
import { onMounted ,ref} from 'vue';
import Quiz from './components/Quiz.vue';

const quiz = ref(null)
const state = ref('loading')

onMounted(() => {
  fetch('/quiz.json')
  .then(r =>{
    if(r.ok)
        return r.json()
    else
      throw new Error("impossible de charger le json !")
  })
  .then(data => {
    quiz.value = data
    state.value = 'idle'

  }).catch(e =>{
    state.value = 'error'
  })
})
</script>


<style scoped>
.container{
  margin-top: 2rem;
}
</style>
