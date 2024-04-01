<script >
import questions from '@/seeds/questions.json'
export default {
    data(){
        return{
            questions:questions,
            selectedIndex: 0,
            selectedAnswer: null,
            question: questions[0],
            userAnswers: []
        }
    },
    methods: {
        nextQuestion(){
            if(this.selectedAnswer !== null){
                const question =this.question


                this.userAnswers.push({
                    question: this.selectedIndex,
                    answer: this.question.options[this.selectedAnswer]
                });

                this.selectedIndex += 1;
                this.question = questions[this.selectedAnswer]

                this.selectedAnswer = null;
            }

        },
        selectAnswer(index){
            this.selectedAnswer = index
        }
    }
}
</script>

<template>
  <div class="container" style="margin-top: 10px">
      <div class="problem" v-if="questions.length > selectedIndex">
          <p>

              <b>Задание {{selectedIndex+1}} из {{ questions.length }}:</b>
          </p>
          <p style="margin-top: 10px">
              <b>{{question.title}}</b>
          </p>
          <p style="margin-bottom: 10px">
              {{question.descr}}
          </p>


          <p class="selectAnswerText">
              <b>Выберите правильный ответ: </b>
          </p>
          <label class="answer" v-for="(answer, index) in question.options" @click="selectAnswer(index)">
              <input type="radio" :name="'answer' + selectedIndex" :value="index" v-model="selectedAnswer"
                     style="width: auto; margin-bottom: 0px">
              <p>{{ answer.title }}</p>
          </label>
          <button class="btn btnDefault" @click="nextQuestion">Далее</button>

      </div>
      <div class="problem" v-else>
          <h1 v-for="userAnswer in userAnswers">{{userAnswer.question+1}}: {{userAnswer.answer.title}}</h1>
      </div>

  </div>
</template>

<style>
.card{
    background-color: #aaffaa;
}
.problem{
    background-color: #aaffaa;
    box-shadow: black;
    padding: 10px;
    border-radius: 10px;
    margin-bottom: 10px;
}
.selectAnswerText{
    margin-bottom: 10px;
}
.answer{
    display: flex;
    justify-items: center;
    gap: 5px;
    align-items: center;
}
</style>
