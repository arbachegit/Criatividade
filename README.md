<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Interativo com Risk</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        .card {
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 600px;
            overflow: hidden;
        }
        .card-content {
            padding: 20px;
        }
        .message {
            display: flex;
            align-items: flex-start;
            margin-bottom: 20px;
        }
        .avatar {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            margin-right: 15px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 24px;
            flex-shrink: 0;
        }
        .message-content {
            background-color: #e5e5e5;
            border-radius: 18px;
            padding: 10px 15px;
            max-width: calc(100% - 65px);
        }
        .user-message {
            flex-direction: row-reverse;
        }
        .user-message .avatar {
            margin-right: 0;
            margin-left: 15px;
        }
        .user-message .message-content {
            background-color: #dcf8c6;
        }
        .options {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .option-button {
            background-color: #4CAF50;
            border: none;
            color: white;
            padding: 15px 32px;
            text-align: left;
            text-decoration: none;
            display: flex;
            align-items: center;
            font-size: 16px;
            cursor: pointer;
            border-radius: 8px;
            transition: background-color 0.3s;
        }
        .option-button:hover {
            background-color: #45a049;
        }
        .option-button:disabled {
            background-color: #cccccc;
            cursor: not-allowed;
        }
        .loading {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 50px;
        }
        .loading-dot {
            width: 10px;
            height: 10px;
            background-color: #333;
            border-radius: 50%;
            margin: 0 5px;
            animation: bounce 0.6s infinite alternate;
        }
        .loading-dot:nth-child(2) {
            animation-delay: 0.2s;
        }
        .loading-dot:nth-child(3) {
            animation-delay: 0.4s;
        }
        @keyframes bounce {
            to {
                transform: translateY(-10px);
            }
        }
        @media (max-width: 480px) {
            .card {
                max-width: 100%;
                border-radius: 0;
            }
            .card-content {
                padding: 10px;
            }
            .avatar {
                width: 40px;
                height: 40px;
                font-size: 20px;
            }
            .message-content {
                max-width: calc(100% - 55px);
            }
            .option-button {
                padding: 10px 20px;
            }
        }
    </style>
</head>
<body>
    <div id="quiz-container" class="card">
        <div class="card-content">
            <!-- Quiz content will be dynamically inserted here -->
        </div>
    </div>
    <script>
        const quizData = {
            question: "Eu posso desenvolver a minha capacidade criativa?",
            options: [
                { id: 1, text: “A criatividade é uma habilidade inata em muitas pessoas, mas é um dom que apenas algumas conseguem desenvolver plenamente e explorar em todo o seu potencial.”},
                { id: 2, text: "A criatividade é resultado do esforço e da persistência. As pessoas não nascem criativas, elas se tornam criativas ao longo de suas jornadas." }
            ],
            correctAnswer: 2
        };
        let step = 0;
        let selectedAnswer = null;
        let isCorrect = null;
        function renderQuiz() {
            const container = document.querySelector('.card-content');
            container.innerHTML = '';
            // Render question
            container.appendChild(createMessage('Risk pergunta:', quizData.question, '🤖', '#3498db'));
            if (step === 0) {
                // Render options
                const optionsContainer = document.createElement('div');
                optionsContainer.className = 'options';
                quizData.options.forEach(option => {
                    const button = document.createElement('button');
                    button.className = 'option-button';
                    button.innerHTML = `
                        <div class="avatar" style="background-color: #2ecc71; color: white; margin-right: 10px;">😊</div>
                        ${option.text}
                    `;
                    button.onclick = () => handleSelectAnswer(option.id);
                    optionsContainer.appendChild(button);
                });
                container.appendChild(optionsContainer);
            }
            if (step >= 1 && selectedAnswer) {
                // Render user answer
                const selectedOption = quizData.options.find(opt => opt.id === selectedAnswer);
                container.appendChild(createMessage('Resposta:', selectedOption.text, '😊', '#2ecc71', true));
            }
            if (step === 1) {
                // Render loading animation
                const loading = document.createElement('div');
                loading.className = 'loading';
                loading.innerHTML = '<div class="loading-dot"></div><div class="loading-dot"></div><div class="loading-dot"></div>';
                container.appendChild(loading);
            }
            if (step === 2) {
                // Render final answer
                const correctOption = quizData.options.find(opt => opt.id === quizData.correctAnswer);
                const message = `
                    <p>${isCorrect ? 'Parabéns! Você acertou!' : 'Ops! Não foi dessa vez.'}</p>
                    <p>A resposta correta é: <strong>${correctOption.text}</strong></p>
                    <p>A criatividade é impulsionada pela obstinação, um dos comportamentos essenciais para expandir sua capacidade de imaginar e desenvolver ideias. Sem determinação, vontade e propósito, não há evolução nem criação.</p>
                `;
                container.appendChild(createMessage('Risk responde:', message, '🤖', isCorrect ? '#2ecc71' : '#e74c3c'));
            }
        }
        function createMessage(title, content, avatar, bgColor, isUser = false) {
            const messageDiv = document.createElement('div');
            messageDiv.className = `message${isUser ? ' user-message' : ''}`;
            messageDiv.innerHTML = `
                <div class="avatar" style="background-color: ${bgColor}; color: white;">${avatar}</div>
                <div class="message-content">
                    <p><strong>${title}</strong></p>
                    <p>${content}</p>
                </div>
            `;
            return messageDiv;
        }
        function handleSelectAnswer(answerId) {
            selectedAnswer = answerId;
            isCorrect = answerId === quizData.correctAnswer;
            step = 1;
            renderQuiz();
            setTimeout(() => {
                step = 2;
                renderQuiz();
            }, 5000);
        }
        // Initial render
        renderQuiz();
    </script>
</body>
</html>
