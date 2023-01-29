<script setup>
// const props = defineProps(["text", "titol"])
    // defineProps({
    //     titol: String,
    //     text: String
    // })
    defineProps(["dades"])
</script>

<template>
    <!--<h1>{{ props.titol }}</h1>-->
    <!--<h2>{{ props.text }}</h2>-->
    <!--<h1>{{ titol }}</h1>
        <h2>{{ text }}</h2>-->
    <h1>{{ dades.titol }}</h1>
    <h2>{{ dades.text }}</h2>
</template>

<style scoped>
</style>