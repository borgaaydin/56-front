<template>
  <div>
    <div v-on:click="check(response)"
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
    props: ['response', 'index', 'locked'],
    data () {
      return {
        checked: false,
        correct: false
      }
    },
    methods: {
      check: function (response) {
        if (this.$parent.$parent.locked) return
        this.checked = true
        let i = this.$parent.$parent.questionIndex
        if (response === this.$parent.$parent.quiz[i].dogruCevap) {
          this.$parent.$parent.locked = true
          this.correct = true
          this.$parent.$parent.totalCorrect += 1
          let self = this
          setTimeout(function () {
            self.$parent.$parent.locked = false
            self.$parent.$parent.questionIndex++
          }, 600)
        } else {
          this.$parent.$parent.locked = true
          this.correct = false
          let self = this
          setTimeout(function () {
            self.$parent.$parent.locked = false
            self.$parent.$parent.questionIndex++
          }, 600)
        }
      },
      checkQuestion: function () {
        this.checked = true
      }
    },
    computed: {
      isCorrect () {
        return this.correct && this.checked
      },
      isWrong () {
        return !this.correct && this.checked
      }
    },
    created: function () {
      if (this.response === this.$parent.$parent.quiz[this.index].dogruCevap) {
        this.correct = true
      } else {
        this.correct = false
      }

      this.checked = false
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .answer span {
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

  .answer div.incorrect span {
    background-color: rgba(255, 0, 0, 0.18);
  }

  .answer div.correct span {
    background-color: rgba(0, 128, 0, 0.22);
  }

  .answer span:hover {
    -webkit-box-shadow: 0px 4px 10px -4px rgba(0,0,0,0.02);
    -moz-box-shadow: 0px 4px 10px -4px rgba(0,0,0,0.02);
    box-shadow: 0px 4px 10px -4px rgba(0,0,0,0.02);
  }

  .answer span input {
    display: none;
  }
</style>
