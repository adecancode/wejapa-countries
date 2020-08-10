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
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
