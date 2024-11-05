<html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz WhatsApp</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #e5ddd5;
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        .chat-container {
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
            width: 100%;
            max-width: 400px;
            overflow: hidden;
        }
        .chat-header {
            background-color: #075e54;
            color: white;
            padding: 10px;
            text-align: center;
            font-weight: bold;
        }
        .chat-messages {
            padding: 20px;
            display: flex;
            flex-direction: column;
        }
        .message {
            max-width: 80%;
            margin-bottom: 10px;
            padding: 8px 12px;
            border-radius: 8px;
            position: relative;
            clear: both;
        }
        .bot-message {
            background-color: #dcf8c6;
            align-self: flex-start;
        }
        .user-message {
            background-color: #e1ffc7;
            align-self: flex-end;
        }
        .options {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-top: 10px;
        }
        .option {
            background-color: #f0f0f0;
            border: none;
            padding: 10px;
            border-radius: 8px;
            cursor: pointer;
            text-align: center;
        }
        .option.selected {
            background-color: #25d366;
            color: white;
        }
        .loading {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 20px;
        }
        .loading-dot {
            width: 8px;
            height: 8px;
            background-color: #b3b3b3;
            border-radius: 50%;
            margin: 0 4px;
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
                transform: translateY(-4px);
            }
        }
    </style>
</head>
<body>
    <div class="chat-container">
        <div class="chat-header">Quiz WhatsApp</div>
        <div class="chat-messages">
            <div class="message bot-message">
                <p>Qual é a capital do Brasil?</p>
                <div class="options">
                    <button class="option">Rio de Janeiro</button>
                    <button class="option">São Paulo</button>
                    <button class="option selected">Brasília</button>
                    <button class="option">Salvador</button>
                </div>
            </div>
            <div class="message user-message">
                <p>Brasília</p>
            </div>
            <div class="message bot-message">
                <div class="loading">
                    <div class="loading-dot"></div>
                    <div class="loading-dot"></div>
                    <div class="loading-dot"></div>
                </div>
            </div>
            <div class="message bot-message">
                <p>A resposta correta é: <strong>Brasília</strong></p>
                <p>Brasília é a capital do Brasil desde 1960, quando foi inaugurada para substituir o Rio de Janeiro como sede do governo federal.</p>
            </div>
            <div class="message bot-message">
                <p>✅ Parabéns por participar da questão!</p>
            </div>
        </div>
    </div>
</body>
</html>
