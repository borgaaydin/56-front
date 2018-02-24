<template>
  <div>
    <div v-for="(response, index) in question.cevaplar">
        <quiz-option v-on:click.native="showCorrectAnswer()" :response="response" :index="qindex" class="answer"></quiz-option>
    </div>
  </div>

</template>

<script>
  import QuizOption from './QuizOption.vue'

  export default {
    components: {QuizOption},
    name: 'quiz-question',
    props: ['question', 'qindex', 'locked'],
    data () {
      return {
        checked: false,
        correct: false
      }
    },
    methods: {
      showCorrectAnswer: function () {
        for (let child of this.$children) {
          if (child.correct) child.checked = true
        }
      }
    },
    computed: {
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
