<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Site Educacional Interativo</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Aprenda de Forma Interativa</h1>
        <p>Responda às perguntas para testar seus conhecimentos!</p>
    </header>

    <main>
        <section class="question-container">
            <p id="question">Qual é a capital da França?</p>
            <ul id="options">
                <li onclick="checkAnswer(this, 'Paris')">Paris</li>
                <li onclick="checkAnswer(this, 'Londres')">Londres</li>
                <li onclick="checkAnswer(this, 'Berlim')">Berlim</li>
                <li onclick="checkAnswer(this, 'Roma')">Roma</li>
            </ul>
            <button onclick="nextQuestion()">Próxima Pergunta</button>
            <p id="feedback"></p>
        </section>
    </main>

    <script src="script.js"></script>
</body>
</html>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f9;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    color: #333;
}

header {
    text-align: center;
    margin-bottom: 20px;
}

.question-container {
    background-color: #fff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    text-align: center;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    background-color: #e0e0e0;
    margin: 10px 0;
    padding: 10px;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
}

li:hover {
    background-color: #d0d0d0;
}

button {
    margin-top: 15px;
    padding: 10px 20px;
    background-color: #4caf50;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #45a049;
}

#feedback {
    margin-top: 15px;
    font-weight: bold;
}
// Array de perguntas e respostas corretas
const questions = [
    { question: "Qual é a capital da França?", answer: "Paris", options: ["Paris", "Londres", "Berlim", "Roma"] },
    { question: "Qual é a capital do Brasil?", answer: "Brasília", options: ["São Paulo", "Brasília", "Rio de Janeiro", "Salvador"] },
    { question: "Qual é a capital do Japão?", answer: "Tóquio", options: ["Pequim", "Tóquio", "Seul", "Bangkok"] },
];

let currentQuestionIndex = 0;

// Carregar a primeira pergunta
function loadQuestion() {
    const questionElement = document.getElementById("question");
    const optionsElement = document.getElementById("options");
    const feedbackElement = document.getElementById("feedback");

    // Limpa o feedback e opções
    feedbackElement.textContent = "";
    optionsElement.innerHTML = "";

    // Carrega a pergunta atual
    const currentQuestion = questions[currentQuestionIndex];
    questionElement.textContent = currentQuestion.question;

    // Adiciona as opções como elementos de lista
    currentQuestion.options.forEach(option => {
        const li = document.createElement("li");
        li.textContent = option;
        li.onclick = () => checkAnswer(li, currentQuestion.answer);
        optionsElement.appendChild(li);
    });
}

// Verifica a resposta e exibe o feedback
function checkAnswer(selectedOption, correctAnswer) {
    const feedbackElement = document.getElementById("feedback");

    if (selectedOption.textContent === correctAnswer) {
        feedbackElement.textContent = "Correto!";
        feedbackElement.style.color = "green";
    } else {
        feedbackElement.textContent = "Errado! Tente novamente.";
        feedbackElement.style.color = "red";
    }
}

// Carrega a próxima pergunta
function nextQuestion() {
    currentQuestionIndex++;

    if (currentQuestionIndex < questions.length) {
        loadQuestion();
    } else {
        document.getElementById("question").textContent = "Parabéns! Você completou todas as perguntas.";
        document.getElementById("options").innerHTML = "";
        document.getElementById("feedback").textContent = "";
    }
}

// Inicializa o questionário
loadQuestion();
