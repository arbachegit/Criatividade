<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Interativo com Robôs</title>
    <script src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
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
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        function QuizInterativo() {
            const [step, setStep] = React.useState(0);
            const [selectedAnswer, setSelectedAnswer] = React.useState(null);
            const [isCorrect, setIsCorrect] = React.useState(null);

            const quizData = {
                question: "Qual é a capital do Brasil?",
                options: [
                    { id: 1, text: "Rio de Janeiro" },
                    { id: 2, text: "Brasília" }
                ],
                correctAnswer: 2
            };

            const handleSelectAnswer = (answerId) => {
                setSelectedAnswer(answerId);
                setStep(1);
                setIsCorrect(answerId === quizData.correctAnswer);
            };

            React.useEffect(() => {
                if (step === 1) {
                    const timer = setTimeout(() => {
                        setStep(2);
                    }, 5000);
                    return () => clearTimeout(timer);
                }
            }, [step]);

            return (
                <div className="card">
                    <div className="card-content">
                        <div className="message">
                            <div className="avatar" style={{backgroundColor: '#3498db', color: 'white'}}>🤖</div>
                            <div className="message-content">
                                <p>{quizData.question}</p>
                            </div>
                        </div>

                        {step === 0 && (
                            <div className="options">
                                {quizData.options.map((option) => (
                                    <button
                                        key={option.id}
                                        className="option-button"
                                        onClick={() => handleSelectAnswer(option.id)}
                                    >
                                        <div className="avatar" style={{backgroundColor: '#2ecc71', color: 'white', marginRight: '10px'}}>🤖</div>
                                        {option.text}
                                    </button>
                                ))}
                            </div>
                        )}

                        {step >= 1 && selectedAnswer && (
                            <div className="message user-message">
                                <div className="avatar" style={{backgroundColor: '#2ecc71', color: 'white'}}>🤖</div>
                                <div className="message-content">
                                    <p>{quizData.options.find(opt => opt.id === selectedAnswer)?.text}</p>
                                </div>
                            </div>
                        )}

                        {step === 1 && (
                            <div className="loading">
                                <div className="loading-dot"></div>
                                <div className="loading-dot"></div>
                                <div className="loading-dot"></div>
                            </div>
                        )}

                        {step === 2 && (
                            <div className="message">
                                <div className="avatar" style={{backgroundColor: isCorrect ? '#2ecc71' : '#e74c3c', color: 'white'}}>
                                    {isCorrect ? '😃' : '😢'}
                                </div>
                                <div className="message-content">
                                    <p>
                                        {isCorrect ? 'Parabéns! Você acertou!' : 'Ops! Não foi dessa vez.'}
                                    </p>
                                    <p>
                                        A resposta correta é: <strong>{quizData.options.find(opt => opt.id === quizData.correctAnswer)?.text}</strong>
                                    </p>
                                    <p>
                                        Brasília é a capital do Brasil desde 1960, quando foi inaugurada para substituir o Rio de Janeiro como sede do governo federal.
                                    </p>
                                </div>
                            </div>
                        )}
                    </div>
                </div>
            );
        }

        ReactDOM.render(<QuizInterativo />, document.getElementById('root'));
    </script>
</body>
</html>
