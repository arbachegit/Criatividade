<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GitHub Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            color: #333;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }
        h1 {
            color: #0366d6;
        }
        #quiz {
            background-color: #f6f8fa;
            border: 1px solid #e1e4e8;
            border-radius: 6px;
            padding: 20px;
            margin-top: 20px;
        }
        button {
            background-color: #2ea44f;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 16px;
            margin-top: 10px;
        }
        button:hover {
            background-color: #2c974b;
        }
        #result {
            margin-top: 20px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h1>GitHub Quiz</h1>
    <div id="quiz">
        <h2 id="question"></h2>
        <div id="choices"></div>
        <button id="submit">Submit Answer</button>
    </div>
    <div id="result"></div>

    <script>
        const quizData = [
            {
                question: "What does Git stand for?",
                choices: ["Global Information Tracker", "Gobal Internet Technology", "Graphical Interface Tool", "None of the above"],
                correctAnswer: 3
            },
            {
                question: "Which command is used to create a new Git repository?",
                choices: ["git start", "git init", "git new", "git create"],
                correctAnswer: 1
            },
            {
                question: "What is a 'fork' in GitHub?",
                choices: ["A bug in the code", "A copy of a repository", "A branch in a repository", "A merge conflict"],
                correctAnswer: 1
            }
        ];

        let currentQuestion = 0;
        let score = 0;

        const questionEl = document.getElementById("question");
        const choicesEl = document.getElementById("choices");
        const submitBtn = document.getElementById("submit");
        const quizEl = document.getElementById("quiz");
        const resultEl = document.getElementById("result");

        function loadQuestion() {
            const question = quizData[currentQuestion];
            questionEl.textContent = question.question;

            choicesEl.innerHTML = "";
            for (let i = 0; i < question.choices.length; i++) {
                const choice = question.choices[i];
                choicesEl.innerHTML += `
                    <div>
                        <input type="radio" id="choice${i}" name="answer" value="${i}">
                        <label for="choice${i}">${choice}</label>
                    </div>
                `;
            }
        }

        function getSelected() {
            const answerEls = document.querySelectorAll("input[name='answer']");
            for (const answerEl of answerEls) {
                if (answerEl.checked) {
                    return parseInt(answerEl.value);
                }
            }
            return undefined;
        }

        submitBtn.addEventListener("click", () => {
            const answer = getSelected();
            if (answer !== undefined) {
                if (answer === quizData[currentQuestion].correctAnswer) {
                    score++;
                }

                currentQuestion++;
                if (currentQuestion < quizData.length) {
                    loadQuestion();
                } else {
                    quizEl.style.display = "none";
                    resultEl.innerHTML = `
                        <h2>You finished the quiz!</h2>
                        <p>Your score: ${score}/${quizData.length}</p>
                    `;
                }
            }
        });

        loadQuestion();
    </script>
</body>
</html>
