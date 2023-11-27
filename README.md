<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Questionário</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
        }

        #quiz-container {
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
            width: 400px;
        }

        .question {
            font-size: 18px;
            margin-bottom: 10px;
        }

        .options label {
            display: block;
            margin-bottom: 10px;
        }

        #user-info input {
            width: 100%;
            padding: 8px;
            margin-bottom: 10px;
        }

        button {
            background-color: #4caf50;
            color: white;
            padding: 10px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

        button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>

<div id="quiz-container">
    <div id="user-info">
        <label for="userName">Nome:</label>
        <input type="text" id="userName" placeholder="Digite seu nome">

        <label for="userDOB">Data de Nascimento:</label>
        <input type="date" id="userDOB">
    </div>

    <div class="question" id="question"></div>
    <div class="options" id="options"></div>
    <button onclick="checkAnswer()">Verificar Resposta</button>
</div>

<script>
    const questions = [
        {
            question: "Qual é a capital do Brasil?",
            options: ["São Paulo", "Rio de Janeiro", "Brasília", "Salvador"],
            correctAnswer: "Brasília"
        },
        {
            question: "Quem escreveu 'Dom Quixote'?",
            options: ["Miguel de Cervantes", "William Shakespeare", "Jane Austen", "Fyodor Dostoevsky"],
            correctAnswer: "Miguel de Cervantes"
        }
    ];

    let currentQuestion = 0;

    function loadQuestion() {
        const questionElement = document.getElementById('question');
        const optionsElement = document.getElementById('options');

        questionElement.textContent = questions[currentQuestion].question;

        optionsElement.innerHTML = "";

        questions[currentQuestion].options.forEach((option, index) => {
            const input = document.createElement('input');
            input.type = "radio";
            input.name = "option";
            input.value = option;
            input.id = `option${index}`;

            const label = document.createElement('label');
            label.textContent = option;
            label.setAttribute('for', `option${index}`);

            optionsElement.appendChild(input);
            optionsElement.appendChild(label);
        });
    }

    function checkAnswer() {
        const userName = document.getElementById('userName').value;
        const userDOB = document.getElementById('userDOB').value;

        if (!userName || !userDOB) {
            alert("Por favor, preencha seu nome e data de nascimento.");
            return;
        }

        const selectedOption = document.querySelector('input[name="option"]:checked');
        if (selectedOption) {
            const userAnswer = selectedOption.value;
            const correctAnswer = questions[currentQuestion].correctAnswer;

            if (userAnswer === correctAnswer) {
                alert(`Olá ${userName}! Resposta correta!`);
            } else {
                alert(`Olá ${userName}! Resposta incorreta. A resposta correta é: ${correctAnswer}`);
            }

            currentQuestion++;

            if (currentQuestion < questions.length) {
                loadQuestion();
            } else {
                alert("Questionário concluído!");
                resetQuiz();
            }
        } else {
            alert("Por favor, selecione uma opção.");
        }
    }

    function resetQuiz() {
        currentQuestion = 0;
        loadQuestion();
    }

    // Inicializar o questionário
    loadQuestion();
</script>

</body>
</html>
