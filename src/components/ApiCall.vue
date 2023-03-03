<template>
    <div>
        <h1 v-html="question"></h1>
        <template v-if="answers">
            <template v-for="answer, index in answers" :key="index">
            <input type="radio" name="options" :value="answer" v-model="chosenAns" :disabled="answerSubmitted"/>
            <label v-html="answer"></label>
            <br />
            </template>
            {{ msg }}
            <br/>
            <button @click="submitAns()">Submit</button>
            <button @click="nextQue()">Next Question</button>
        </template>
    </div>
</template>
<script>
export default {
  name: 'ApiCall',
  data(){
    return{
        question: undefined,
        incorrectAns: undefined,
        correctAns: undefined,
        chosenAns: undefined,
        msg: undefined,
        answerSubmitted: false,
    }
  },
  computed:{
    answers() {
        let answers = this.incorrectAns && JSON.parse( JSON.stringify( this.incorrectAns ) );
        this.incorrectAns && answers.splice( Math.round( Math.random() * answers.length ),0,this.correctAns);
        return answers;
    }
  },
  created(){
    this.nextQue()
    }, 
  methods:{
    submitAns(){
        if(!this.chosenAns){
            this.msg = "Please select at least one!!!"
        }else{
            this.answerSubmitted = true;
            if(this.chosenAns === this.correctAns){
            this.msg = "Your Answer is Correct";
            }else{
                this.msg = `Sorry, wrong Answer!!! The correct answer is "${this.correctAns}"`;
            }
        }  
    },
    nextQue(){    
        this.axios.get(`https://opentdb.com/api.php?amount=1&category=18`).then( (response) => {
        this.msg = '';
        this.answerSubmitted = false;
        this.chosenAns = '';      
        this.question = response.data.results[0].question;
        this.incorrectAns = response.data.results[0].incorrect_answers;
        this.correctAns = response.data.results[0].correct_answer;
    })
    }
  }  
}
</script>