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
      background: url("http://gipsypixel.com/wp-content/uploads/2017/11/Pokemon-Desktop-Backgrounds-All-Background-Wallpaper-For-Laptop-Hd-Images.png") 0 0 no-repeat fixed;
      background-size: 100% 100%;
      width: 100vw;
      height: 100vh;

    }
</style>
