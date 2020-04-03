<template>
  <div class="container">
    <b-jumbotron>
      <!-- <template v-slot:header>Question #</template> -->

      <template v-slot:lead>
        <!-- {{console.log(currentQuestion)}} -->
        {{currentQuestion.question}}
      </template>

      <hr class="my-4" />
      <!-- 
      <p v-for="(answere, index) in answers" :key="index">
        {{answere}}
      </p>-->
      <b-list-group>
        <b-list-group-item @click="selectAnswer(index)" :class="[selectedIndex === index ? 'selected' : '']" v-for="(answere, index) in shuffledAnswers" :key="index">{{answere}}</b-list-group-item>
      </b-list-group>

      <b-button variant="primary" @click="submitAnswere">Subtmit</b-button>
      <b-button variant="success" @click="next">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from 'lodash'
export default {
  props: {
    currentQuestion: Object,
    next: Function
  },
  data(){
    return  {
      selectedIndex: null,
      shuffledAnswers: []
    }
  },
  computed: {
    answers() {
      let answers = [...this.currentQuestion.incorrect_answers];
      // answers.push(this.currentQuestion.correct_answere);
      answers.push(this.currentQuestion.correct_answer);
      return answers;
    }
  },
  watch: {
    currentQuestion() {
      this.selectedIndex = null;
      this.shuffleAnswers();

    }
  },
  methods: {
    selectAnswer(index){
      this.selectedIndex = index;
    },
    shuffleAnswers(){
      let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer];
      this.shuffledAnswers = _.shuffle(answers);
    },
    submitAnswere(){
      let isCorrect = false;
      if(this.selectedIndex === this.correctIndex){
        isCorrect = true;
      }
      return isCorrect;
    }
  },
  mounted() {
    this.shuffleAnswers()
  }
};
</script>

<style scoped>
  .list-group-item {
    margin-bottom: 15px;
  }
  .list-group-item:hover{
    background-color: silver;
    cursor: pointer;
  }
  .correct  {
    background-color: greenyellow;
  }
  .incorrect  {
    background-color: red;
  }
  .selected {
    background-color: skyblue;
  }
</style>

