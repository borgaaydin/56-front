<template>
  <div class="container" id="app">
    <div class="logo">
      <img srcset="./assets/elli6_logo.png" src="./assets/elli6_logo.png" alt="elli6">
    </div>
    <transition name="">
      <div class="landing" v-show="landing">
        <h1 class="landing-title">
          Sınırsız
          <br>

          <span>
            Edebiyat Soruları
          </span>
        </h1>
        <h2 class="landing-subtitle">
          Her yerden erişebileceğin <br>
          ücretsiz edebiyat soru bankası
        </h2>
        <button class="startButton" v-on:click="openQuiz">
          Hemen Başla
        </button>
      </div>
    </transition>
    <transition name="fade">
      <quiz-creator class="quiz-wrapper" v-show="!landing"></quiz-creator>
    </transition>
  </div>
</template>

<script>
  import QuizCreator from './components/QuizCreator.vue'
  export default {
    name: 'app',
    components: {
      QuizCreator
    },
    data () {
      return {
        landing: true
      }
    },
    methods: {
      openQuiz: function (event) {
        this.landing = false
        document.getElementById('body').classList.remove('landing')
      }
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: rgba(43, 102, 118, 1);
  }

  html {
    font-family: 'Lora', serif;
    height: 100%;
    overflow: hidden;

    background: rgba(255, 254, 240, 1);

  }

  body {
    margin: 0;
    height: 100%;

    -webkit-transition: background-image 0.5s ease-in-out;
    transition: background-image 0.5s ease-in-out;
  }

  body.landing {
    background-image: url(../static/behcet-necatigil.png), url(../static/aziz-nesin.png);
    background-position: left bottom, right bottom;
    background-repeat: no-repeat, no-repeat;
  }

  ul {
    padding: 0;
    margin: 0;
    list-style: none;
  }

  #app {
    width: 100%;
    max-width: 1000px;
    margin: 40px auto;
    text-align: center;
  }

  .logo img {
    height: 100px;
  }

  .quiz-wrapper {
    width: 320px;
    margin: 0 auto;
  }

  .landing {
    font-family: 'Libre Baskerville', serif;
  }

  .landing-title {
    width: 100%;
    text-align: left;
    font-size: 90px;
    line-height: 60px;
    margin-bottom: 0;
  }

  .landing-title span {
    font-size: 60px;
  }

  .landing-subtitle {
    width: 100%;
    text-align: left;
    color: #76502B;
  }

  .startButton {
    width: 240px;
    height: 54px;
    margin: 100px auto;
    cursor: pointer;
    outline: 0;

    display: flex;
    align-items: center;
    justify-content: center;

    border: 0;
    border-radius: 4px;
    background-color: #2B6676;
    color: #F6F6F6;

    font-size: 24px;

    -webkit-box-shadow: 0px 6px 10px 0px rgba(43,88,118,0.5);
    -moz-box-shadow: 0px 6px 10px 0px rgba(43,88,118,0.5);
    box-shadow: 0px 6px 10px 0px rgba(43,88,118,0.5);

  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
  }
  .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
    opacity: 0;
  }

  @media (max-width: 900px) {
    .logo img {
      height: 60px;
    }

    .landing {
      padding: 0 10px;
    }

    h1.landing-title {
      font-size: 36px;
      line-height: 24px;
    }

    .landing-title span {
      font-size: 24px;
    }

    .landing-subtitle {
      font-size: 20px;
    }

    body.landing {
      background: none;
    }
  }
</style>
