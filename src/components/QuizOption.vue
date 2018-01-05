<template>
  <div>
    <div v-on:click="check(response)"
         v-for="response in question.cevaplar"
         :disabled="locked"
         v-model="checked"
         :value="response"
         :class="{'correct': isCorrect, 'incorrect': isWrong}">
        <span>
            {{response}}
        </span>
    </div>
  </div>

</template>

<script>
  export default {
    name: 'quiz-option',
    props: ['question', 'locked'],
    data () {
      return {
        checked: false,
        correct: false
      }
    },
    methods: {
      check: function (response) {
        if (this.$parent.locked) return
        this.checked = true
        let i = this.$parent.questionIndex
        if (response === this.$parent.quiz[i].dogruCevap) {
          this.$parent.locked = true
          this.correct = true
          this.$parent.totalCorrect += 1
          let self = this
          setTimeout(function () {
            self.$parent.locked = false
            self.$parent.questionIndex++
          }, 600)
        } else {
          this.$parent.locked = true
          this.correct = false
          let self = this
          setTimeout(function () {
            self.$parent.locked = false
            self.$parent.questionIndex++
          }, 600)
        }
      }
    },
    computed: {
      isCorrect () {
        return this.correct && this.checked
      },
      isWrong () {
        return !this.correct && this.checked
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

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
