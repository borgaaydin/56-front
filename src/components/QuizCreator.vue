<template>
  <div>
    <div v-show="!isReady">
      <h3>
        Lütfen soru tipini seçin
      </h3>
      <ul class="questionTypes">
        <li>
          Eser / Yazar
        </li>
        <li>
          Yazar / Eser
        </li>
      </ul>
    </div>
    <Quiz :is-ready="isReady"
          :data-source="dataSource"></Quiz>
  </div>
</template>
<script>
  import Quiz from './Quiz'
  export default {
    name: 'quiz-creator',
    props: [],
    components: {
      Quiz
    },
    data () {
      return {
        isReady: false,
        dataSource: 'http://127.0.0.1:8000/api/quiz/eser/yazar'
      }
    },
    methods: {
      updateSource: function () {
        this.$http.get('https://elli6.com/api/quiz/')
          .then(response => {
            this.quiz = response.data.quiz
          })
      }
    },
    created: function () {
      this.updateSource()
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .questionTitle {
    font-weight: normal;
  }

  .questionTitle strong {
    font-weight: bold;
  }

  .questionBox button {
    background-color: #FE7675; /* Green */
    border: none;
    color: white;
    padding: 8px 24px;
    border-radius: 16px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    cursor: pointer;
    outline:0;

    -webkit-box-shadow: 0px 4px 5px -2px rgba(254,118,117,0.3);
    -moz-box-shadow: 0px 4px 5px -2px rgba(254,118,117,0.3);
    box-shadow: 0px 4px 5px -2px rgba(254,118,117,0.3);
  }

  .buttons {
    margin-top: 20px;
  }

  .prevQuestion {
    float: left;
  }

  .nextQuestion {
    float: right;
  }

  .answerList {
    margin: 10px 0;
  }

  .answerList span {
    width: calc(100% - 40px);
    display: inline-block;
    background-color: #ffffff;
    border: 1px solid rgba(242, 242, 242, 0.62);
    margin-bottom: 10px;
    padding: 10px 20px;
    cursor: pointer;
    text-align: left;

    -webkit-box-shadow: 0px 4px 10px -4px rgba(0,0,0,0.1);
    -moz-box-shadow: 0px 4px 10px -4px rgba(0,0,0,0.1);
    box-shadow: 0px 4px 10px -4px rgba(0,0,0,0.1);
  }

  .answerList div.incorrect span {
    background-color: rgba(255, 0, 0, 0.18);
  }

  .answerList div.correct span {
    background-color: rgba(0, 128, 0, 0.22);
  }

  .answerList span:hover {
    -webkit-box-shadow: 0px 4px 10px -4px rgba(0,0,0,0.02);
    -moz-box-shadow: 0px 4px 10px -4px rgba(0,0,0,0.02);
    box-shadow: 0px 4px 10px -4px rgba(0,0,0,0.02);
  }

  .answerList span input {
    display: none;
  }
</style>
