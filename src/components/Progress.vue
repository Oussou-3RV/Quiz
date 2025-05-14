<template>
    <div>
        Etape : {{ valeur+1 }} / {{ max+1 }}
        <progress :value="valeur" :max="max"></progress>
        
    </div>
</template>

<script setup>


defineProps({
    valeur:Number,
    max:Number
})
</script>