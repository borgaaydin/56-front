<template>
  <div>

    <div v-show="!isReady">
      <h3>
        Soru tipini seçin
      </h3>
      <ul class="questionTypes">
        <li v-for="(type, index) in typeList"
            v-on:click="typeSelector(type)"
            v-show="!typeChosen">
          <span>
            {{ type.name }}
          </span>
        </li>
      </ul>
      <ul class="questionPeriod" v-show="typeChosen && typeChosen.hasPeriod">
        <li v-for="(period, index) in periodList"
            v-on:click="periodSelector(period)">
          {{ period.name }}
        </li>
      </ul>
    </div>
    <Quiz :is-ready="isReady"
          :data-source="dataSource"
          :quiz="quiz"
          :loading="loading"></Quiz>
    <pulse-loader :loading="loading" :color="pulsecolor" :size="pulsesize"></pulse-loader>
  </div>
</template>
<script>
  import Quiz from './Quiz'
  import typeList from './type_list'
  import periodList from './period_list'
  import PulseLoader from 'vue-spinner/src/PulseLoader.vue'

  export default {
    name: 'quiz-creator',
    props: [],
    components: {
      Quiz,
      PulseLoader

    },
    data () {
      return {
        quiz: [],
        isReady: false,
        dataSource: 'https://elli6.com/api/quiz/',
        typeList,
        periodList,
        typeChosen: null,
        periodChosen: '',
        pulsecolor: '#2B6676',
        pulsesize: '24px',
        loading: false
      }
    },
    methods: {
      updateSource: function () {
        this.isReady = !this.isReady
        this.loading = true
        this.$http.get(this.dataSource)
          .then(response => {
            this.loading = false
            this.quiz = response.data.quiz
          })
      },
      typeSelector: function (type) {
        this.typeChosen = type
        this.dataSource += type.url
        if (!type.hasPeriod) {
          this.updateSource()
        }
      },
      periodSelector: function (period) {
        this.periodChosen = period
        this.dataSource += period.id
        this.updateSource()
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

  .questionTypes li,
  .questionPeriod li{
    height: 40px;
    margin-bottom: 10px;
    border: 2px solid #2c3e50a6;
    border-radius: 4px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
  }

  .questionTypes li:hover,
  .questionPeriod li:hover{
    color: white;
    background-color: #FE7675;
    border-color: #FE7675;
  }

  .questionTypes li span,
  .questionPeriod li span{

  }

  .questionPeriod {
    padding: 0 10px;
  }

  .v-spinner {
    margin-top: 100px;
  }
</style>
