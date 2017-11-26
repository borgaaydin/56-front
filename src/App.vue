<template>
  <div class="container" id="app">
    <Quiz></Quiz>
  </div>
</template>

<script>
  import Quiz from './components/Quiz'
  export default {
    name: 'app',
    components: {
      Quiz
    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

html {
  font-family: 'Lora', serif;
  height: 100%;
  overflow: hidden;

  background: rgba(208, 233, 253, 0.41);

}

body {
  margin: 0;
}

ul {
  padding: 0;
  margin: 0;
  list-style: none;
}

#app {
  width: 320px;
  margin: 40px auto;
  text-align: center;
}

</style>
