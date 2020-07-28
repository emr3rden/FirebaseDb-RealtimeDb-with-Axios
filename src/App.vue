<template>

  <div id="app">
    <onSubmit></onSubmit>
  </div>

</template>



<script>

  import onSubmit from './components/onSubmit.vue'

  export default {

    name: 'App',

    components: {
      onSubmit
    },



  }

</script>



<style>

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 20px;
  }



</style>