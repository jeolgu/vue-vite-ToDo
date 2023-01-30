<script setup>
import NovaTasca from './components/NovaTasca.vue'
import Tasques from './components/Tasques.vue'

// Mètodes per a realitzar l'app Vue vite
// CREACIO DE TASQUEST
function comprovarErrors(descripcio, prioritat){
  let obj = {
      error: false,
      msg_error: ""
  };

  obj.error = (descripcio.trim() != "" && prioritat != "") ? false : true;

  if (descripcio.trim() == "") obj.msg_error = "La descripció es obligatoria \n";
  if (prioritat.trim() == "") obj.msg_error += "La prioritat es obligatoria \n";

  return obj;
}
function afegir(descripcio, prioritat){

  let objError = comprovarErrors(descripcio.value, prioritat.value);
  if (objError.error) return alert(objError.msg_error);

  let tasques = [];
  if (localStorage.llistaTasques) tasques = JSON.parse(localStorage.llistaTasques);

  let llistaIds = tasques.map(function(a) { return a.id; });
  let nouId = 1;
  if(llistaIds.length > 0) {
    let maxId = Math.max(...llistaIds);
    nouId = maxId + 1;
  }

  tasques.push({
      id: nouId,
      descripcio: descripcio.value,
      creacio: new Date(),
      prioritat: prioritat.value,
      completada: false
  });

  localStorage.llistaTasques = JSON.stringify(tasques);

  alert("Tasca creada amb éxit");
}

// INICI PROGRAMA
let tasques = [];
if (localStorage.llistaTasques) tasques = JSON.parse(localStorage.llistaTasques);

// LLISTAT DE TASQUES

// CANVIAR PRIORITAT (ALTA MITA o BAIXA)
function canviarPrioritat(id, novaPrioritat) {

  let novaLlista = tasques;
  novaLlista.forEach(function(a) {
      if (a.id === id) {
          a.prioritat = novaPrioritat;
      }
  });

  tasques = novaLlista;
  localStorage.llistaTasques = JSON.stringify(novaLlista);
  //reordenarLlistat(novaLlista);
}

// CANVIAR ESTAT (COMPLETAT-ACTIU, ACTIU-COMPLETAT)
function canviarEstat(id, completada) {

  let novaLlista = tasques;
  novaLlista.forEach(function(a) {
      if (a.id === id) {
          a.completada = completada;
      }
  });

  tasques = novaLlista;
  localStorage.llistaTasques = JSON.stringify(novaLlista);
  //reordenarLlistat(novaLlista);
  //totalTasques = tasques.length;
  //totalTasquesCompletades = tasques.filter(function(a) { if (a.completada) return true; }).length;
}

// ESBORRAR UNA TASCA
function esborrarTasca(id) {
    // PER  ELIMINAR FILTRAREM TOTS ELS QUE NO COINCIDISQUEN AMB EL id QUE ENVIEM. (D'AQUESTA MANERA FEM UN BORRAT SIMULAT)
    let arrLlista = JSON.parse(localStorage.llistaTasques);
    let novaLLista = arrLlista.filter(function(a) { if (a.id != id) return true; });

    tasques = novaLLista;
    // GUARDEM EN EL LOCALSTORAGE PER A QUE "GUARDE EL BORRAT"
    localStorage.llistaTasques = JSON.stringify(novaLLista);
    //totalTasques = tasques.length;
    //totalTasquesCompletades = tasques.filter(function(a) { if (a.completada) return true; }).length;
}

</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <!-- APP To-DO en VUE vite-->
      <!--<NovaTasca @afegirTasca="afegir" />-->
      <Tasques 
        :llistaTasques="tasques" 
        @canviarPrioritat="canviarPrioritat" 
        @canviarEstat="canviarEstat" 
        @esborrarTasca="esborrarTasca" 
        ref="text"/>
    </div>
  </header>

  <main>
    <!--<TheWelcome />-->
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
  width: 100vw;
  height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
