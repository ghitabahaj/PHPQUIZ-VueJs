<template>
  <div class="container game" id="game">
    <div style="width: 100%;">
      <div id="hud">
        <div id="hud-item">
          <p id="progressText" class="hud-prefix">{{ progressText }}</p>
          <div id="progressBar">
            <div :style="progress" id="progressBarFull"></div>
          </div>
        </div>
        <div id="hud-item">
          <p class="hud-prefix">Score</p>
          <h1 class="hud-main-text">{{ score }}</h1>
        </div>
      </div>
      <div class="content">
        <h2 id="question">{{ question }}</h2>
      </div>
      <div class="answers">
        <div v-for="(choice, index) in choices" :key="index" class="choice-container">
          <p class="choice-prefix">{{ choice.prefix }}</p>
          <div @click="getAnswer(index)" class="choice-text" :data-number="choice.number">{{ choice.text }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    answers:{
      type:Array , required:true
    }
  },
  data() {
    return {
      isDisabled : false,
      progressText: "",
      score: 0,
      currentQuestionIndex: 0,
      questions: [
        {
          question: "What is the syntax of a for loop in PHP?",
          choices: [
            { prefix: "A", text: "for (i = 0; i < count; i++)" },
            { prefix: "B", text: "for (i = 0; i <= count; i++)" },
            { prefix: "C", text: "for (i <= 0; i < count; i++)" },
            { prefix: "D", text: "for (i <= 0; i <= count; i++)" }
          ],
          correctAnswer: 1
        },
        {
          question: "What is the output of the following PHP code? echo 4 + '2' * 3;",
          choices: [
            { prefix: "A", text: "10" },
            { prefix: "B", text: "8" },
            { prefix: "C", text: "6" },
            { prefix: "D", text: "Error" }
          ],
          correctAnswer: 2
        },
        {
          question: "What is the difference between the 'echo' and 'print' statements in PHP?",
          choices: [
          { prefix: "A", text: "There is no difference, they both output text to the screen." },
          { prefix: "B", text: "The 'echo' statement is faster than 'print'." },
          { prefix: "C", text: "The 'print' statement can only output strings, while 'echo' can output any data type." },
          { prefix: "D", text: "The 'echo' statement returns a value, while 'print' does not." }
          ],
          correctAnswer: 2
          },
          {
          question: "What is the syntax of a for loop in PHP?",
          choices: [
            { prefix: "A", text: "for (i = 0; i < count; i++)" },
            { prefix: "B", text: "for (i = 0; i <= count; i++)" },
            { prefix: "C", text: "for (i <= 0; i < count; i++)" },
            { prefix: "D", text: "for (i <= 0; i <= count; i++)" }
          ],
          correctAnswer: 1
        },
        {
          question: "What is the output of the following PHP code? echo 4 + '2' * 3;",
          choices: [
            { prefix: "A", text: "10" },
            { prefix: "B", text: "8" },
            { prefix: "C", text: "6" },
            { prefix: "D", text: "Error" }
          ],
          correctAnswer: 2
        },
        {
          question: "What is the difference between the 'echo' and 'print' statements in PHP?",
          choices: [
          { prefix: "A", text: "There is no difference, they both output text to the screen." },
          { prefix: "B", text: "The 'echo' statement is faster than 'print'." },
          { prefix: "C", text: "The 'print' statement can only output strings, while 'echo' can output any data type." },
          { prefix: "D", text: "The 'echo' statement returns a value, while 'print' does not." }
          ],
          correctAnswer: 2
          },
      ],
    };
  },
  computed: {
    progress(){
      return "width:"+ ((this.currentQuestionIndex +1) / this.questions.length) * 100+"%;";
    },
    question() {
      return this.questions[this.currentQuestionIndex].question;
    },
    choices() {
      return this.questions[this.currentQuestionIndex].choices;
    }
  },
  methods: {
    getAnswer(index) {
      if(!this.isDisabled){
      this.isDisabled = true;
      let answer = {
        question: this.currentQuestionIndex,
        correct : this.questions[this.currentQuestionIndex].correctAnswer,
        chosen: index+1
      }
      this.answers.push(answer);

      if (index+1 === this.questions[this.currentQuestionIndex].correctAnswer) {
        this.score += 10;
        document.getElementsByClassName("choice-text")[index].classList.add("correct");
      } else {
        document.getElementsByClassName("choice-text")[index].classList.add("incorrect");
      }

      setTimeout(() => {
        
        document.getElementsByClassName("choice-text")[index].classList.remove("incorrect");
        document.getElementsByClassName("choice-text")[index].classList.remove("correct");


        this.isDisabled=false;

        if (this.currentQuestionIndex === this.questions.length-1) {
          this.progressText = "Quiz Completed";
          
          this.$emit("show-result", this.score);
        }else{
          this.currentQuestionIndex++;

          
        }
      }, 1500);
      
    }}
  }
};

</script>

  <style>

  @import url("https://fonts.googleapis.com/css2?family=Catamaran&display=swap");
* {
  font-family: "Catamaran", sans-serif;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  text-align: center;
}

  .choice-container {
  display: flex;
  justify-content: center;
  margin: auto;
  margin-bottom: 0.5rem;
  margin-top: 1.5rem;
  width: 60%;
  font-size: 1rem;
  border: 0.1rem solid rgba(86, 165, 235, 0.25);
  background-color: white;
  display: flex;
  justify-content: space-between;
  padding-left: 1em;
}
.choice-container:hover {
  cursor: pointer;
  box-shadow: 0 0.4rem 1.4rem 0 rgba(86, 185, 235, 0.5);
  transform: translateY(-0.1rem);
  transition: transform 150ms;
}

.choice-prefix {
  color: navy;
  width: 5%;
}

.choice-text {
  width: 95%;
}

#hud {
  display: flex;
  justify-content: space-around;
}

.hud-prefix {
  text-align: center;
  font-size: 1.3rem;
}

#progressBar {
  width: 10rem;
  height: 2rem;
  border: 0.2rem solid #a0a7c1;
  border-radius: 1em;
  margin-top: 1.5rem;
  margin-bottom: 1.5rem;
}

#progressBarFull {
  height: 1.7rem;
  background-color: #a0a7c1;
  border-radius: 1em;
  width: 0%;
  transition: all 0.3 ease;
}
.content {
  background-color: lightsteelblue;
  width: 65%;
  margin: auto;
  height: 4em;
  border-radius: 2em;
  display: flex;
  justify-content: center;
  align-items: center;
  color: ghostwhite;
  padding-top: 1em;
  padding-bottom: 1em;
}

.correct {
  background-color: rgba(56, 204, 91, 0.7921568627);
}

.incorrect {
  background-color: rgba(231, 72, 88, 0.6823529412);
}


  </style>
  