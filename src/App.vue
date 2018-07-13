<template>
  <div id="app">

    <Pokemon />
  </div>
</template>

<script>
import Pokemon from './components/Pokemon.vue'

export default {
  name: 'app',
  components: {
    Pokemon
  }
}
</script>

<style>
    @import url('https://fonts.googleapis.com/css?family=Orbitron');
    @import url("https://fonts.googleapis.com/icon?family=Material+Icons");

    *{
        margin:0;
        padding: 0;
        font-family: 'Orbitron', sans-serif;
        font-size: 16px;
    }

    body{
        position: relative;
      background: url("https://amazingpict.com/wp-content/uploads/2014/03/Cute-Pokemon-Yellow-Background-Desktop.jpg") 0 0 no-repeat fixed;
      background-size: 100% 100%;

    }
</style>
