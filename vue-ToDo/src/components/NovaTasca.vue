<script setup>
    import {ref} from 'vue'

    let llistaPrioritats = ["alta", "mitja", "baixa"]
    let descripcio = ref("")
    let prioritat = ref("")
    const emit = defineEmits(["afegirTasca"])
    function afegirTasca(){
        emit("afegirTasca", descripcio, prioritat)
        descripcio.value = ""
        prioritat.value = ""
    }
</script>

<template>
      <label for="descripcio">Descripció</label>
        <input id="descripcio" class="form-control" type="text" v-model="descripcio" maxlength="100" />
        <label for="prior">Prioritat</label>
        <select id="prior" class="form-select" v-model="prioritat">
            <option v-for="prioritat in llistaPrioritats" :value="prioritat">
                {{ prioritat }}
            </option>
        </select>
        <br />
        <button class="btn btn-primary" @click="afegirTasca">Afegeix la tasca</button>
</template>

<style scoped>


input,
select {
    max-width: 50vw;
    margin-bottom: 10px;
}

</style>