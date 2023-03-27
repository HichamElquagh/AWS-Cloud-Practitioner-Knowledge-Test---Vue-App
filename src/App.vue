<script setup>
import{ref , computed } from 'vue'
// import ProgressBar  from './components/ProgressBar.vue'
const questions = ref([
   { 
      question: 'what is vue js ? ',
      answer:0,
      options:[
        'A front end framwork',
        'A library',
        'A package',
      ],
      selected: null
    },
     
    { 
      question: 'what is ? ',
      answer:2,
      options:[
        'A front end ',
        'A library',
        'A package',
      ],
      selected: null
    },

    { 
      question: 'what is vue js ? ',
      answer:1,
      options:[
        'A front end framwork',
        'A library',
        'A package',
      ],
      selected: null
    },   
    { 
      question: 'what is vue js ? ',
      answer:1,
      options:[
        'A front end framwork',
        'A library',
        'A package',
      ],
      selected: null
    },  
    { 
      question: 'what is vue js ? ',
      answer:0,
      options:[
        'A front end framwork',
        'A library',
        'A package',
      ],
      selected: null
    },   
])
const quizComplited = ref(false)
const currentQuestion= ref(0)
const score = computed(()=>{
    let value = 0
    questions.value.map( q =>{
      if(q.selected == q.answer){
        value++
      }
    })
return value 

})
const getCurrentQuestion = computed(() => {
  let question = questions.value[currentQuestion.value]
    question.index = currentQuestion.value
    return question
})
const SetAnsewer = evt =>{
  questions.value[currentQuestion.value].selected = evt.target.value
  evt.target.value = null
}

const NextQuestion = ()=>{
  if ( currentQuestion.value < questions.value.length-1){
    currentQuestion.value++
  } else{
    quizComplited.value= true
  }
}
</script>

<template>
  <div class="parApp">
  <main class="app" >
    <h1>The Quiz</h1>
    <ProgressBar/>
    <section class="quiz" v-if="!quizComplited">
      <div class="quiz-info">
        <span class="question">{{ getCurrentQuestion.question}}</span>
        <span class="score">Score {{score}}/{{questions.length}}</span>
      </div>
      <div class="options">
        <label v-for="(option, index) in getCurrentQuestion.options"
        :key="index"
        :class="`option ${
         getCurrentQuestion.selected == index
          ? (getCurrentQuestion.answer == index ? 'correct' : 'wrong')
         : ''
        }${
          getCurrentQuestion.selected != null && index != getCurrentQuestion.selected ? 'disabled' : ''}`">
          <input type="radio"
          :name="getCurrentQuestion.index"
          :value="index"
          v-modal="getCurrentQuestion.selected"
          :disabled="getCurrentQuestion.selected"
          @change="SetAnsewer">
          <span>{{ option }}</span>
          
        </label>
      </div>
      <button 
      @click="NextQuestion"
      :disabled="!getCurrentQuestion.selected">
      {{ 
        getCurrentQuestion.index == questions.length -1
        ? 'Finish'
        : getCurrentQuestion.selected==null
        ? 'Select an option'
        : 'Next Question'
      }}
      </button>

    </section> 
    <section class="sectionFinishQuiz" v-else>
      <h2 class="finishQuiz" >You have finished the quiz!</h2>
      <p class="resultScore">Your score is {{ score }}/{{ questions.length}}</p>
    </section>
  </main>
</div>
</template>

<style scoped>
.parApp{
  display: flex;
  justify-content: center;
  width: 75vw;
}
.app {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 2rem;

    /* min-height: 100vh; */
    width: 100vh;
}
h1{
  font-size: 2rem;
  margin-bottom: 2rem;
}
.quiz{
  background-color: rgb(71, 71, 142);
  padding: 1rem;
  width: 100%;
  max-width: 640px;
  border-radius:0.5rem ;
}
.quiz-info{
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}
.quiz-info .question{
  color:beige;
  font-size: 1.25rem;
}

.quiz-info .score{
  color: azure;
  font-size: 1.25rem;
}

.options{
  margin-bottom: 1rem;
}
.option{
  display: block;
  padding:1rem;
  background-color:rgb(27, 27, 31);
  margin-bottom:0.5rem;
  border-radius: 0.5rem;
  cursor: pointer;

}
option:hover {
  background-color:#ece9f0 ;
}
.option.correct {
  background-color: rgb(82, 176, 143);
}
.option.wrong {
  background-color:rgb(169, 52, 52) ;
}
.option:last-of-type{
  margin-bottom: 0;
}
.option.disabled{
  opacity: 0.5;
}
.option input {
  display: none;
}
button{
  appearance: none;
  outline: none;
  border: none ;
  cursor:pointer;
  padding: 0.5rem 1rem;
  background-color: aquamarine;
  color: #2d213f;
  font-weight: 700;
}
.sectionFinishQuiz{
   
  background-color: rgb(71, 71, 142);
  padding: 2rem;
  border-radius: 1rem;
}
.finishQuiz{
  text-align: center;
  margin-bottom: 1rem;
}
.resultScore{
  font-size: 2rem;
  background-color: #2d213f;
  border: #ece9f0;
  border-radius: 1rem ;
  padding: 0.2rem 3rem;
  text-align: center;

}

 * {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
 }
 body{
    color: aliceblue;
    width: 100vh;
 }
</style>
