<template>
  <div id="app">
    <Header />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3" >
          <QuestionBox 
            v-if="question.length"
            :currentQuestion = "questions[index]"
            :next="next"
          />
        </b-col>
      </b-row>
    </b-container>
    <Tutorials />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from "./components/QuestionBox"
import Tutorials from './components/Tutorials.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox,
    Tutorials
  },
  data: function(){
    return {
      questions: [],
      index:0
    }
  },

  methods:{
    next(){
      this.index++;
    }
  },

  mounted: function(){
    fetch("https://opentdb.com/api.php?amount=10&category=27&type=multiple", {
      method: "get"
    })
    .then((response) => {return response.json()})
    .then((jsonData) =>  {
      this.questions = jsonData.results;
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
