# Quiz-APP
I created basic quiz app.


HTML part
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Quiz App</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="app">
        <h1>Simple Quiz</h1>
        <div class="quiz">
            <h2 id="question">Question goes here :)</h2>
            <div id="answer-buttons">
                <button class="btn">Answer 1</button>
                <button class="btn">Answer 2</button>
                <button class="btn">Answer 3</button>
                <button class="btn">Answer 4</button>
            </div>
            <button id="next-btn">Next Question</button>
        </div>
    </div>
    <script src="script.js"></script>
</body>
</html>

CSS part
* {
    margin: 0;
    padding: 0;
    font-size: 'Popins' , sans-serif;
    box-sizing: border-box;
}
body{
    background-color: #E29E25;
}
.app {
    background-color: #fff;
    width: 90%;
    max-width: 500px;
    margin: 100px auto 0;
    border-radius: 10px;
    padding: 30px;
}
.app h1{
    font-weight: 600;
    color: #7a3c4e;
    border-bottom: 1px solid #333;
    padding-bottom: 30px;
}
.quiz{
    padding: 20px 0;
}
.quiz h2{
    font-size: 18px;
    font-weight: 600;
    color: #a5b512;
}
.btn{
    background: #fff;
    color: #222;
    font-weight: 500;
    width: 100%;
    border: 1px solid #222;
    padding: 10px;
    margin: 10px 0;
    text-align: left;
    border-radius: 4px;
    cursor: pointer;
}
.btn:hover:not([disabled]){
    color: #fff;
    background: #222;
}
.btn:disabled{
    cursor: no-drop;
}
#next-btn{
    background: #a5a5;
    color: #fff;
    font-weight: 500;
    width: 150px;
    border: 0;
    padding: 10px;
    margin: 20px auto;
    border-radius: 20px 60px;
    cursor: pointer;
    display: none;
}
.correct{
    background: #9aeabc;
}
.incorrect{
    background: #ff9393;


JavaScript part (Don't worry about the nonsense of the questions, I just gave them as an example.)
const questions = [
    {
        question: "Which is largest animal in the world",
        answers: [
            { Text:"Shark", correct: false},
            { Text:"Blue whale", correct: true},
            { Text:"Elephant", correct: false},
            { Text:"Giraffe", correct: false},
        ]
    },
    {
        question: "Which is the most I hate it",
        answers: [
            { Text:"tea", correct: false},
            { Text:"alchaol", correct: true},
            { Text:"pizza", correct: false},
            { Text:"soda", correct: false},
        ]
    },
    {
        question: "Which is the most samllest contient in the world",
        answers: [
            { Text:"Asia", correct: false},
            { Text:"australia", correct: true},
            { Text:"africa", correct: false},
            { Text:"artic", correct: false},
        ]
    },
    {
        question: "Which is the most I love it",
        answers: [
            { Text:"flormar", correct: false},
            { Text:"fenty", correct: true},
            { Text:"rare beuty", correct: false},
            { Text:"maybelinne", correct: false},
        ]
    },
];

const questionElement = document.getElementById("question");
const answerButton = document.getElementById("answer-buttons");
const nextButton = document.getElementById("next-btn");

let currentQuestionIndex = 0;
let score = 0;

function startQuiz() {
    currentQuestionIndex = 0;
    score = 0;
    nextButton.innerHTML = "Next";
    showQuestion();
}

function showQuestion(){
    resetState();
    let currentQuestion = questions[currentQuestionIndex];
    let questionNo = currentQuestionIndex + 1;
    questionElement.innerHTML = questionNo + "." + currentQuestion.answers.
    question;

    currentQuestion.answers.forEach(answer => {
        const button = document.createElement("button");
        button.innerHTML = answer.Text;
        button.classList.add("btn");
        answerButton.appendChild(button);
        if(answer.correct){
            button.dataset.correct = answer.correct;
        }
        button.addEventListener("click", selectAnswer);
    });
}

function resetState(){
    nextButton.style.display = "none";
    while(answerButton.firstChild){
        answerButton.removeChild(answerButton.firstChild);
    }
}

function selectAnswer(e){
    const selectedBtn = e.target;
    const isCorrect = selectedBtn.dataset.correct === "true";
    if(isCorrect){
        selectedBtn.classList.add("correct");
        score++;
    }else {
        selectedBtn.classList.add("incorrent");
    }
    Array.from(answerButton.children).forEach(button => {
        if(button.dataset.correct === "true"){
            button.classList.add("correct");
        }
        button.disabled = true;
    });
    nextButton.style.display = "block";
}

function showScore(){
    resetState();
    questionElement.innerHTML = `You scored ${score} out of ${questions.
        length}!`;
        nextButton.innerHTML = "Play Again";
        nextButton.style.display = "block";
}

function handleNextButton(){
    currentQuestionIndex++;
    if(currentQuestionIndex < questions.length){
        showQuestion();
    }else{
        showScore();
    }
}

nextButton.addEventListener("click" , ()=>{
    if(currentQuestionIndex < questions.length){
        handleNextButton();
    }else{
        startQuiz();
    }
});

startQuiz();
