<script setup>
// import HelloWorld from './components/HelloWorld.vue'
// import TheWelcome from './components/TheWelcome.vue'
import Tasques from './components/Tasques.vue'
// var variable = "Jesus prova"
// var variable2 = {titol: "titol nou", text: "nou text per a VUE"}
function mostrarConsola(){
  console.log("has fet click")
}
function mostrarConsola2(){
  console.log("Has fet click en m2")
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <!--<HelloWorld msg="You did it!" />-->
      <!--<Tasques text="Prova1 primera prova entrada de text" titol="Entrada 1" />-->
      <!--<Tasques text="Prova1 primera prova entrada de text" :titol="variable" />-->
      <!--<Tasques text="Prova 2 text diferent per a un altra entrada" titol="Entrada 2" />-->
      <!--<Tasques :dades="variable2" @eventmostrar="mostrarConsola" />-->
      <Tasques @eventMostrar="mostrarConsola" @m2="mostrarConsola2"/>
      <!--<Tasques @miEvento="mostrar"/>-->
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
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
