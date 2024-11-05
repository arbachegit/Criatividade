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
            max-width: 600px;
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
        .choice {
            margin-bottom: 10px;
        }
        .correct {
            color: #22863a;
        }
        .incorrect {
            color: #cb2431;
        }
    </style>
</head>
<body>
    <h1>GitHub Quiz</h1>
    <div id="quiz">
        <h2 id="question">What does Git stand for?</h2>
        <div id="choices">
            <div class="choice">
                <input type="radio" id="choice0" name="answer" value="0">
                <label for="choice0">Global Information Tracker</label>
            </div>
            <div class="choice">
                <input type="radio" id="choice1" name="answer" value="1">
                <label for="choice1">Global Internet Technology</label>
            </div>
            <div class="choice">
                <input type="radio" id="choice2" name="answer" value="2">
                <label for="choice2">Graphical Interface Tool</label>
            </div>
            <div class="choice">
                <input type="radio" id="choice3" name="answer" value="3">
                <label for="choice3">None of the above</label>
            </div>
        </div>
        <button id="submit">Submit Answer</button>
    </div>
    <div id="result"></div>

    <script>
        const correctAnswer = 3;
        const submitBtn = document.getElementById("submit");
        const resultEl = document.getElementById("result");
        const choicesEl = document.getElementById("choices");

        submitBtn.addEventListener("click", () => {
            const selectedAnswer = document.querySelector('input[name="answer"]:checked');
            if (selectedAnswer) {
                const answer = parseInt(selectedAnswer.value);
                const isCorrect = answer === correctAnswer;
                
                // Disable all radio buttons
                document.querySelectorAll('input[name="answer"]').forEach(input => {
                    input.disabled = true;
                });

                // Highlight correct and incorrect answers
                choicesEl.querySelectorAll('.choice').forEach((choice, index) => {
                    if (index === correctAnswer) {
                        choice.classList.add('correct');
                    } else if (index === answer && !isCorrect) {
                        choice.classList.add('incorrect');
                    }
                });

                // Show result
                resultEl.textContent = isCorrect ? "Correct! " : "Incorrect. ";
                resultEl.textContent += "Git doesn't actually stand for anything. It's not an acronym, but rather a word that Linus Torvalds chose for its meaning in British slang: 'a stupid person'.";
                
                // Disable submit button
                submitBtn.disabled = true;
            }
        });
    </script>
</body>
</html>
