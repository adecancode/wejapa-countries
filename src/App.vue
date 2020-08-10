<template>
  <div id="app">
    <CountryDirectories />
  </div>
</template>

<script>
import CountryDirectories from './components/CountryDirectories.vue'

export default {
  name: 'App',
  components: {
    CountryDirectories
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  background: #f9f9f9;
  font-family: 'Poppins', sans-serif;
}
</style>
