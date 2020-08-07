<template>
  <div id="app">
   <a href="https://logo-logos.com/harry-potter-logo-610.html">
   <img src="https://logo-logos.com/wp-content/uploads/2016/10/Harry_Potter_logo_text_logotype.png" alt="Harry Potter logo" />
   </a>
    <CharacterPage/>
  </div>
</template>

<script>
import CharacterPage from './components/characterPage'

export default {
  name: 'App',
  components: {
    CharacterPage
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
