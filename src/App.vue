<template>
  <div id="app">
    <Header 
      :numCorrect="numCorrect"
      :numTotal="numTotal"
      :resetQ="resetQ"
    />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox
            v-if="questions.length && !quizEnd" 
            :currentQuestion="questions[index]"
            :next="next"
            :increment="increment"
          />
          <QuizResults
          v-if="quizEnd"
          :numCorrect="numCorrect"
          :numTotal="numTotal"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
import QuizResults from './components/QuizResults.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox,
    QuizResults
  },
  data() {
    return {
      questions : [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
      quizEnd: false
    }
  },
  methods: {
    next() {
      if(this.index < 9) {
        this.index++
      } else {
        this.quizEnd = true
      }
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++
      }
      this.numTotal++
    },
    resetQ() {
      this.index = 0
      this.numCorrect = 0
      this.numTotal = 0
    }
  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple', {
      method: 'get'
    })
    .then((response) => {
      return response.json()
    })
    .then((jsonData) => {
      this.questions = jsonData.results
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
