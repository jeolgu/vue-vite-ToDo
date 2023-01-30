<script setup>
// const props = defineProps(["text", "titol"])
    // defineProps({
    //     titol: String,
    //     text: String
    // })
    // defineProps(["dades"])
    // const emit = defineEmits(["eventmostrar"])
    // function mostraLog(){
    //     emit("eventmostrar")
    // }
    const emit = defineEmits(['eventMostrar', 'm2'])
    function fesClick(){
        emit('eventMostrar')
    }
    function metodoDelEvento(){
        emit('m2')
    }
</script>

<template>
    <!--<h1>{{ props.titol }}</h1>-->
    <!--<h2>{{ props.text }}</h2>-->
    <!--<h1>{{ titol }}</h1>
        <h2>{{ text }}</h2>-->
    <!--<h1>{{ dades.titol }}</h1>
    <h2>{{ dades.text }}</h2>-->
    <button @click="metodoDelEvento"> Fes-me click </button>
    <button @click="fesClick">click me</button>
</template>

<style scoped>
</style>