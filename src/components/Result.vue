<template>
 <div class="result" id="result"> 
  <p>You've completed the Quiz!</p>
    <p>Your Score is {{ score }}</p>
    <button  @click="$emit('quitQuiz')">Quit Quiz</button>

     <p> Your Answers</p>
    <div v-for="answer in answers" :key="answer.question">
     <p class="content"> question number {{ answer.question }} </p> 
      <p v-if="answer.chosen == answer.correct">correct</p>
      <p v-else>incorrect</p>
    </div>
    </div>
</template>


<script>
export default {
  name: "Result",
  props: {
    score: {
      type: Number,
      required: true
    },
    answers:{
      type:Array , required:true
    }
  }
  
};
</script>


<style>
.result{
  background-color: aliceblue;
  margin: auto;
  width: 75%;
  margin-top: 5em;
  padding: auto;
  padding-top: 2em;
  padding-bottom: 2em;
  box-shadow: 0 0.4rem 1rem 0 rgba(141, 178, 196, 0.5);
}
.result {
  flex-direction: column;
}
.result i {
  font-size: 5em;
  color: darkslateblue;
  margin-bottom: 0.3em;
}
.result p {
  font-size: 1.4em;
  font-weight: bold;
}
.result #score1 {
  color: darkslateblue;
  font-weight: bolder;
  font-size: 3em;
}
.result button {
  background-color: white;
  border-color: darkslateblue;
  color: darkslateblue;
  border-radius: 0.5em;
  padding: 10px 30px;
  font-size: large;
  cursor: pointer;
  width: 150px;
  margin: auto;
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