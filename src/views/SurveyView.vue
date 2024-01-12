<template>
  <main class="app">
    <section class="survey">
      <div v-if="!surveyCompleted" class="info">
        <span class="question">{{ getCurrentQuestion.question }}</span>
        <div class="options">
          <label
            v-for="(option, index) in getCurrentQuestion.options"
            :key="index"
            :class="`option ${getCurrentQuestion.selected === index ? 'selected' : ''} ${
              surveyCompleted ? 'disabled' : ''
            }`"
          >
            <input
              type="radio"
              :name="currentQuestion.valueOf.toString()"
              :value="index"
              v-model="getCurrentQuestion.selected"
              :disabled="surveyCompleted || getCurrentQuestion.selected !== null"
            />
            <span class="option-text">{{ option }}</span>
          </label>
        </div>
      </div>
      <div v-else class="thank-you-message">Thank you for completing the survey!</div>
      <button
        v-if="!surveyCompleted"
        @click="nextQuestion"
        :disabled="getCurrentQuestion.selected === null"
      >
        {{ currentQuestion.valueOf === questions.length - 1 ? 'Finish' : 'Next' }} 
      </button>
    </section>
  </main>
</template>

<script>
import { ref, computed } from 'vue'

export default {
  setup() {
    const questions = ref([
      {
        question: 'How satisfied are you with our service?',
        options: ['1 (Not Satisfied)', '2', '3', '4', '5 (Very Satisfied)'],
        selected: null
      },
      {
        question: 'Would you like to see more features added to our platform?',
        options: ['Yes', 'No'],
        selected: null
      },
      {
        question: 'On a scale of 1 to 5, how satisfied are you with our product/service?',
        options: ['1 (Not Likely)', '2', '3', '4', '5 (Very Likely)'],
        selected: null
      },
      {
        question: 'How easy was it to navigate our website?',
        options: ['1 (Not Likely)', '2', '3', '4', '5 (Very Likely)'],
        selected: null
      },
      {
        question: 'How likely are you to recommend us to a friend?',
        options: ['1 (Not Likely)', '2', '3', '4', '5 (Very Likely)'],
        selected: null
      }
    ])

    const currentQuestion = ref(0)
    const surveyCompleted = ref(false)

    const getCurrentQuestion = computed(() => {
      const currentIdx = currentQuestion.value
      if (currentIdx >= 0 && currentIdx < questions.value.length) {
        const question = questions.value[currentIdx]
        question.index = currentIdx
        return question
      } else {
        return { question: '', options: [], selected: null, index: -1 }
      }
    })

    const nextQuestion = () => {
      if (currentQuestion.value < questions.value.length - 1) {
        currentQuestion.value++
      } else {
        surveyCompleted.value = true
      }
    }

    return { questions, currentQuestion, surveyCompleted, getCurrentQuestion, nextQuestion }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}
body {
  background-color: #271c36;
  color: rgb(248, 248, 238);
}
.survey {
  font-size: medium;
}
input[type='radio'] {
  transform: scale(1.5);
  margin-right: 7px;
  margin: 10px;
}
.option-text {
  font-size: 16px;
  margin-left: 1px;
}
button {
  padding: 1%;
  margin-top: 5%;
  margin-left: 30%;
  border-radius: 6px;
}
@media (min-width: 1024px) {
  .survey {
    min-height: 100vh;
    font-size: medium;
    justify-content: center;
  }
}
</style>
