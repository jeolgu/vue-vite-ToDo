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
    import {ref} from 'vue'

   
    const emit = defineEmits(['eventMostrar', 'm2'])
    var serie = ref([1,2,3])
    function fesClick(){
        emit('eventMostrar')
    }
    function metodoDelEvento(){
        emit('m2', 'parametre')
        serie.value.push(4)
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
    <ul>
        <li v-for="num in serie"> {{ num }}</li>
    </ul>
</template>

<style scoped>
</style>