<script setup>
    import { ref } from 'vue'
    // let totalTasques = 0
    // let totalTasquesCompletades = 0
    // let filtrat =  ""
    const prop = defineProps(["llistaTasques"])
    var llistat = ref(["llistat"])
    const emit = defineEmits(["canviarPrioritat","canviarEstat", "esborrarTasca"])

    function canviarPrioritat(id, novaPrioritat){
        emit("canviarPrioritat", id, novaPrioritat);
        tasques.value = llistaTasques;
    }

    function canviarEstat(id, completada){
        emit("canviarEstat", id, completada )

        llistat.value = prop.llistaTasques;
    }

    function esborrarTasca(id){
        emit("esborrarTasca", id)
        tasques.value = llistaTasques;
    }
    
    // let filtre = ""
    // let opcionsFiltre = [
    //     { id: 1, nom: "" },
    //     { id: 2, nom: "Actives" },
    //     { id: 3, nom: "Completades" },
    //     { id: 4, nom: "Totes" }
    // ]
    // let filtreText = ""

    // ACI POSAREM LES FUNCIONS QUE SEMPRE ES PUGUEN REPETIR I SIGUIEN INTERNES COM ARA EL FORMATEIG DE DATES I MINUTS 
    // DES DE L'INICI JA QUE VOLEM QUE ES CALCULE INTERNAMENT NO DE MANERA GLOBAL COM ARA ELS PROXIMS EVENTS CREATS.
    function formatejarDates(dataTasca) {
        let f = new Date(dataTasca);
        if (dataTasca.includes("Z")) { // CONTÉ ZONA HORARIA, RESTAR-LI LA FRANJA HORARIA
            f = new Date(new Date(dataTasca).getTime() - Math.abs(new Date(dataTasca).getTimezoneOffset() * 60));
        }

        let stringData = f.getDate() + "/" + (f.getMonth() + 1) + "/" + f.getFullYear();
        stringData += " - " + f.getHours() + ":" + ((f.getMinutes() < 10) ? "0" : "") + f.getMinutes() + ":" + ((f.getSeconds() < 10) ? "0" : "") + f.getSeconds();

        return stringData;
    }

    function minutsDesdeInici(dataTasca) {
        let creacioTasca = new Date(dataTasca);
        let dataActual = new Date();
        let diff_milisegons = dataActual.getTime() - creacioTasca.getTime();
        let diff_minuts = diff_milisegons / 1000 / 60;

        return parseInt(diff_minuts) + " min.";
    }

</script>

<template>
    <!--
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
    -->
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
                    <button class="btn btn-danger btn-sm" @click="canviarPrioritat(tasca.id, 'alta')">Alta</button>
                    <button class="btn btn-warning btn-sm" @click="canviarPrioritat(tasca.id, 'mitja')">Mitja</button>
                    <button class="btn btn-success btn-sm" @click="canviarPrioritat(tasca.id, 'baixa')">Baixa</button>
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
    
    <!--
    <div>
        Total tasques: {{ totalTasques }}. Completades: {{ totalTasquesCompletades }} {{ filtrat }}
    </div>
    -->
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