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
    // import {ref} from 'vue'

   
    // const emit = defineEmits(['eventMostrar', 'm2'])
    // var serie = ref([1,2,3])
    // function fesClick(){
        // emit('eventMostrar')
    // }
    // function metodoDelEvento(){
        // emit('m2', 'parametre')
        // serie.value.push(4)
    // }
    // import {ref} from 'vue'

    // let llistaPrioritats = ["alta", "mitja", "baixa"]
    // let descripcio = ref("")
    // let prioritat = ref("")
    // const emit = defineEmits(["afegirTasca"])
    // function afegirTasca(){
    //     emit("afegirTasca", descripcio, prioritat)
    //     descripcio.value = ""
    //     prioritat.value = ""
    // }
    let totalTasques = 0
    let totalTasquesCompletades = 0
    let filtrat =  ""
    let llistaTasques = []
    let filtre = ""
    let opcionsFiltre = [
        { id: 1, nom: "" },
        { id: 2, nom: "Actives" },
        { id: 3, nom: "Completades" },
        { id: 4, nom: "Totes" }
    ]
    let filtreText = ""
</script>

<template>
    <!--<h1>{{ props.titol }}</h1>-->
    <!--<h2>{{ props.text }}</h2>-->
    <!--<h1>{{ titol }}</h1>
        <h2>{{ text }}</h2>-->
    <!--<h1>{{ dades.titol }}</h1>
    <h2>{{ dades.text }}</h2>-->
    <!--<button @click="metodoDelEvento"> Fes-me click </button>
    <button @click="fesClick">click me</button>
    <ul>
        <li v-for="num in serie"> {{ num }}</li>
    </ul>-->
    <!--
    <label for="descripcio">Descripció</label>
        <input id="descripcio" class="form-control" type="text" v-model="descripcio" maxlength="100" />
        <label for="prior">Prioritat</label>
        <select id="prior" class="form-select" v-model="prioritat">
            <option v-for="prioritat in llistaPrioritats" :value="prioritat">
                {{ prioritat }}
            </option>
        </select>

        <button class="btn btn-primary" @click="afegirTasca">Afegeix la tasca</button>
    -->
    <div>
        <div class="header-tasques">
            <label for="mostrar">Filtrar llistat tasques </label>
            <select id="mostrar" class="form-select" v-model="filtre" @change="filtrarLlistat">
            <option v-for="filtre in opcionsFiltre" :value="filtre.id">
                {{ filtre.nom }}
            </option>
        </select>
        </div>
        <div class="header-tasques">
            <label for="filtre-text">Filtrar llistat tasques </label>
            <input type="text" id="filtre-text" class="form-control" v-model="filtreText" @keyup="filtrarTasquesDescripcio" />
        </div>
        <div class="header-tasques centrat">
            <button class="btn btn-primary" @click="eliminarCompletades">El·liminar totes les tasques completades</button>
        </div>
    </div>
    <template v-if="llistaTasques.length">
        <div class="tasca">
            <h2>Llistat TASQUES</h2>
            <table>
            <tr>
                <th>Descripció</th>
                <th>Creació</th>
                <th>Temps aprox.<br>creació</th>
                <th>Prioritat</th>
                <th>Canviar prioritat</th>
                <th>Completar<br>Activar</th>
                <th>El·liminar</th>
            </tr>
            <tr v-for="(tasca, indice) in llistaTasques">
                <td class="descripcio">
                    <span v-bind:class="{completada: tasca.completada}">
                        {{ tasca.descripcio }}
                    </span>
                </td>
                <td class="creacio">{{ formatejarDates(tasca.creacio) }}</td>
                <td>{{ minutsDesdeInici(tasca.creacio) }}</td>
                <td>{{ tasca.prioritat }}</td>
                <td>
                    <button class="btn btn-danger btn-sm" @click="cambiarPrioritat(tasca.id, 'alta')">Alta</button>
                    <button class="btn btn-warning btn-sm" @click="cambiarPrioritat(tasca.id, 'mitja')">Mitja</button>
                    <button class="btn btn-success btn-sm" @click="cambiarPrioritat(tasca.id, 'baixa')">Baixa</button>
                </td>
                <td>
                    <button class="btn btn-info btn-sm" v-if="!tasca.completada" @click="canviarEstat(tasca.id, true)">Completar</button>
                    <button class="btn btn-info btn-sm" v-if="tasca.completada" @click="canviarEstat(tasca.id, false)">Activar</button>
                </td>
                <td><button class="btn btn-dark btn-sm" @click="esborrarTasca(tasca.id)">El·liminar</button></td>
            </tr>                
            </table>
        </div>
    </template>
    <template v-else>
        <h2>No existeixen tasques</h2>
    </template>

    <div>
        Total tasques: {{ totalTasques }}. Completades: {{ totalTasquesCompletades }} {{ filtrat }}
    </div>
</template>

<style scoped>
input,
select {
    max-width: 50vw;
    margin-bottom: 10px;
}


/* REVISAR */


/*
#container {
    height: 90%;
}

.center {
    text-align: center;
}
*/

table,
ul {
    margin-top: 10px;
    margin-bottom: 10px;
}

li {
    margin-bottom: 10px;
}

table,
th,
tr,
td {
    border: 2px solid black;
    border-collapse: collapse;
    text-align: center;
}

td {
    min-width: 125px;
    max-width: 250px;
}

th {
    background-color: beige;
}

td,
th {
    height: 60px;
}

td.descripcio {
    padding: 0px 5px;
}

.header-tasques {
    display: inline-block;
    width: 33%;
}

.centrat {
    text-align: center;
}

.header-tasques .form-control,
.header-tasques .form-select {
    max-width: 250px;
}

td button:first-child {
    margin-left: 25px;
}

button {
    margin-right: 25px;
}

.completada {
    text-decoration: line-through;
    color: blue;
}

.creacio {
    width: 125px;
}
</style>