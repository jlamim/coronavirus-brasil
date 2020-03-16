<template>
  <div id="app">
    <Covid19 />
  </div>
</template>

<script>
import Covid19 from './components/Covid19.vue'

export default {
  name: 'App',
  components: {
    Covid19
  }
}
</script>

<style>
body {
  background: url(assets/bg-page.jpg) no-repeat center transparent;
  background-size: cover;
  background-attachment: fixed;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #ffffff;
}
</style>
