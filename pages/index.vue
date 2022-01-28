<template>
    <div class="scoreboard">
        Punktów: {{points}}
    </div>
    <div class="box">
        <h1 class="question" @dblclick="getQuestion"> {{ currentQuestion.question }} </h1>
        <div class="answers">
            <template v-for="(answer, index) in currentQuestion.answers" :key="answer">
                <button type="button" @click.once="checkAnswer(index, $event)">{{ answer }}</button>
            </template>
        </div>
    </div>    
</template>

<script setup>
import questions from '~/public/questions.json'
const randomizer = array => array.map(a => ({ sort: Math.random(), value: a })).sort((a, b) => a.sort - b.sort).map(a => a.value)

const points = ref(0)

const currentQuestion = ref({
    question: null,
    goodAnswerId: null,
    answers: null
})

function getQuestion(){
    if(document.querySelector('.question')){
        document.querySelector('.question').classList.remove("clickable")
    }
    let randomQuestion = questions[Math.floor(Math.random() * questions.length)]
    let goodAnswer = randomQuestion.answers[0]
    currentQuestion.value.answers = randomizer(randomQuestion.answers)
    currentQuestion.value.question = randomQuestion.question
    currentQuestion.value.goodAnswerId = currentQuestion.value.answers.findIndex((answer)=> answer === goodAnswer)
}
getQuestion()

const checkAnswer = (index, event) => {
    if(index === currentQuestion.value.goodAnswerId){
        event.target.classList.add("good")
        points.value++
        currentQuestion.value.question = `✔ ${currentQuestion.value.question} [ ⏭ ]`
        document.querySelector('.question').classList.add("clickable")
    }else{
        event.target.classList.add("bad")
        points.value--
    }
}
</script>

<style lang="scss">
body{
    min-height: 100vh;
    background:#090B26;
    color: #fff;
    display: flex;
    justify-content: center;
    padding-top: 50px;
}
.box{
    width: 1000px;
    max-width: 100vw;
    line-height: 200%;
}
.question{
    font-size: 1.3em;
    font-family: Poppins, sans-serif;
    font-weight: bold;
    padding: 10px;
}
.clickable{
    cursor: pointer;
    &::after{
        content: "(kliknij dwukrotnie)";
        color: cyan;
        margin-left: 10px;
        font-weight: normal;
        white-space: nowrap;
    }
}
.answers{
    margin-top: 10px;
    border-top: 1px solid #ddd;
    padding-top: 20px;
    display: flex;
    flex-direction: column;
}
.answers button{
    text-align: left;
    margin: 10px;
    border: 2px solid #8D8BC9;
    background-color: transparent;
    color: #fff;
    font-family: Poppins, sans-serif;
    border-radius: 20px;
    padding: 10px;
    padding-left: 20px;
    cursor: pointer;
    transition: background-color 0.4s;
    &:hover,&:focus{
        transition: background-color 0.4s;
        background-color: #eee;
        color: #090B26;
        font-weight: bold;
    }
}
button.good{
    background-color: #46aa3f;
    border-color: #117914;
    font-weight: bold;
    &:hover,&:focus{
        color: #fff;
        background-color: #46aa3f;
        border-color: #117914;
    }
    &::before{
        content: "✅";
        padding-right: 10px;
    }
}
button.bad{
    font-weight: bold;
    border-color: #D82727;
    &:hover,&:focus{
        color: #fff;
        background-color: transparent;
    }
    &::before{
        content: "❌";
        padding-right: 10px;
    }
}
.scoreboard{
    font-family: sans-serif;
    font-size: 0.9em;
    color: #ddd;
}
</style>