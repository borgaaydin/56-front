<template>
  <div v-show="this.isReady">
    <div v-for="(question, index) in quiz">
      <div class="questionBox" v-show="index === questionIndex">
        <h2 class="questionTitle">
          <strong>"{{question.soru}}"</strong> adlı eserin yazarı kimdir?
        </h2>
        <div>
          <quiz-question :question="question" :qindex="index" :locked="locked"></quiz-question>
        </div>
      </div>
    </div>
    <div>
      {{ totalCorrect }} / {{ quizLength }}
    </div>

    <div v-show="questionIndex === quizLength">
      <h2>
        10 soruluk edebiyat maceranız sona erdi!
      </h2>
      <p>
        Notunuz : {{ totalCorrect }} / {{ quizLength }}
      </p>
    </div>
  </div>
</template>
<script>
  import QuizQuestion from './QuizQuestion'
  export default {
    name: 'quiz',
    props: ['dataSource', 'questionType', 'answerType', 'period', 'isReady', 'quiz'],
    components: {
      QuizQuestion
    },
    data () {
      return {
        questionIndex: 0,
        quizLength: 10,
        userResponses: new Array(10),
        totalCorrect: 0,
        hasWrongAnswer: false,
        locked: false
      }
    },
    methods: {
      updateSource: function () {
        this.$http.get(this.dataSource)
          .then(response => {
            this.quiz = response.data.quiz
          })
      }
    },
    created: function () {
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
