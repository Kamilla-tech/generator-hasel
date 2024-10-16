<template>
  <div id="app">
    <PasswordGenerator/>
  </div>
</template>

<script>
  import PasswordGenerator from "./components/PasswordGenerator.vue";
  
  export default {
    name: "App",
    components: {
      PasswordGenerator 
    }
  }
</script>

<style scoped>
  #app {
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
