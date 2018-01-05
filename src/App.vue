<template>
  <div class="container" id="app">
    <div class="logo">
      <img srcset="./assets/elli6_logo.png, ./assets/elli6_logo@2x.png 2x" src="./assets/elli6_logo.png" alt="elli6">
    </div>
    <quiz-creator></quiz-creator>
  </div>
</template>

<script>
  import QuizCreator from './components/QuizCreator.vue'
  export default {
    name: 'app',
    components: {
      QuizCreator
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
