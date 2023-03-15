<template>
    <div class="container">
      <div class="guide" id="guide">
      <h3>PHP Quick Quiz - Guide</h3>
      <div><p class="para">Test your technical knowledge on the spot.</p></div>
      <div><p class="para">Evaluate the correctness of your answers.</p></div>
      <div><p class="para">Randomly picked questions from our database.</p></div>
      <div><p class="para">You can test your PHP skills with Us.</p></div>
      <button @click="$emit('startQuiz')">Start Quiz</button>
    </div>
    </div>
  </template>
  
  <script>
  export default {
};
  </script>
  
  <style>
  .container {
  background-color: aliceblue;
  margin: auto;
  width: 75%;
  margin-top: 5em;
  padding: auto;
  padding-top: 2em;
  padding-bottom: 2em;
  box-shadow: 0 0.4rem 1rem 0 rgba(141, 178, 196, 0.5);
  display: flex;
  flex-direction: column;
  }

button {
  width: 150px;
  background-color: white;
  border-color: darkslateblue;
  color: darkslateblue;
  border-radius: 0.5em;
  padding: 10px 30px;
  font-size: large;
  cursor: pointer;
  margin: auto;
  margin-top: 1em;
}
.guide {
  display: flex;
  flex-direction: column;
}
.guide h3 {
  margin-bottom: 1em;
}
.guide div {
  width: 50%;
  margin: auto;
  display: flex;
  justify-content: space-around;
}
.guide div i {
  margin-right: 1em;
}
.guide div .para {
  font-size: 1.1em;
  width: 80%;
  text-align: center;
}

  </style>
  