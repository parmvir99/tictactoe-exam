<template>
  <div class="">
    <Tictactoe/>
  </div>
</template>

<script>
import Tictactoe from './components/tictactoe.vue'

export default {
  name: 'App',
  components: {
    Tictactoe
  }
}
</script>

<style>
@font-face {
  font-family: 'Rudiment Medium';
  font-style: normal;
  font-weight: normal;
  src: local('Rudiment Medium');
  src: url('assets/fonts/Rudiment.woff') format('opentype');
}
html {
  background:url(assets/bg.png);
}
body {
  font-family:'Rudiment Medium' !important;
  background-color: transparent !important;
}
h1, h2, h3, h4, h5, h6 {
  color:#e0dbd1;
}
</style>
