<template>
    <div class="question">
        <h3>{{ question.question }}</h3>
        <ul>
            <li v-for="choice in question.choices" :key="choice">
                <label for="">
                    <input type="radio" name="answer">
                    {{ choice }}
                    
                </label>
            </li>
        </ul>
    </div>
</template>

<script setup>
defineProps({
    question:Object
})
</script>
<style>
.question{
    padding-top: 2rem;
}
li{
    list-style: none;
}
</style>