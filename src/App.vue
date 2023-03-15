<template>
  <div>
    <Guide v-show="showGuide" @startQuiz="showQuiz = true; showGuide = false" />
    <Quiz v-show="showQuiz" @show-result="showResults" :answers="answers"/>
    <Result v-show="showResult" :score="score" @quitQuiz="showQuiz = false; showGuide = true; showResult = false" :answers="answers"/>
  </div>
</template>

<script>
import Guide from "./components/Guide.vue";
import Quiz from "./components/Quiz.vue";
import Result from "./components/Result.vue";


export default {
  name: "App",
  components: {
    Quiz,
    Guide,
    Result
  },
  data() {
    return {
      showGuide: true,
      showQuiz: false,
      showResult: false,
      score: 0,
      answers:[]
    };
  },
  methods: {
     showResults(score) {
      console.log(score)
      this.showQuiz = false;
      this.showResult = true;
      this.score = score;
    }
  }
};
</script>








