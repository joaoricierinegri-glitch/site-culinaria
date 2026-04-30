<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stimulation Clicker</title>
    <style>
        /* CSS - O visual do jogo */
        body {
            margin: 0;
            height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background: radial-gradient(circle, #1a1a2e, #16213e, #0f3460);
            color: white;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden;
            user-select: none; /* Impede de selecionar o texto ao clicar rápido */
        }

        #stats-container {
            text-align: center;
            margin-bottom: 40px;
            animation: fadeIn 1s ease-in;
        }

        .label {
            font-size: 1.2rem;
            letter-spacing: 3px;
            opacity: 0.7;
        }

        #score {
            font-size: 5rem;
            font-weight: bold;
            display: block;
            text-shadow: 0 0 20px rgba(255, 255, 255, 0.4);
        }

        /* O Botão Estilo Clicker */
        #click-btn {
            width: 180px;
            height: 180px;
            border-radius: 50%;
            border: none;
            background: linear-gradient(145deg, #ff4d4d, #b30000);
            color: white;
            font-size: 1.5rem;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 12px 0 #660000, 0 20px 30px rgba(0,0,0,0.5);
            transition: transform 0.05s;
            outline: none;
        }

        #click-btn:active {
            transform: translateY(10px);
            box-shadow: 0 2px 0 #660000, 0 5px 15px rgba(0,0,0,0.5);
        }

        /* Efeito das Partículas subindo */
        .particle {
            position: absolute;
            pointer-events: none;
            color: #ff4d4d;
            font-weight: bold;
            font-size: 2rem;
            text-shadow: 2px 2px 5px rgba(0,0,0,0.5);
            animation: rise 0.7s ease-out forwards;
        }

        @keyframes rise {
            0% { transform: translateY(0) scale(1); opacity: 1; }
            100% { transform: translateY(-200px) scale(1.5); opacity: 0; }
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>

    <div id="stats-container">
        <span class="label">STIMULATION</span>
        <span id="score">0</span>
    </div>
    
    <button id="click-btn">CLICK!</button>

    <script>
        // JavaScript - A lógica do jogo
        let count = 0;
        const scoreDisplay = document.getElementById('score');
        const btn = document.getElementById('click-btn');

        btn.addEventListener('click', (e) => {
            // Aumenta o contador
            count++;
            scoreDisplay.innerText = count.toLocaleString(); // Adiciona pontos nos milhares

            // Som de clique (opcional, se quiser adicionar um arquivo .mp3 depois)
            // createSound();

            // Cria o efeito visual no local do clique
            createParticle(e.clientX, e.clientY);
            
            // Pequeno tremor na pontuação
            scoreDisplay.style.transform = "scale(1.1)";
            setTimeout(() => scoreDisplay.style.transform = "scale(1)", 50);
        });

        function createParticle(x, y) {
            const p = document.createElement('div');
            p.className = 'particle';
            p.innerText = '+1';
            
            // Centraliza o texto no mouse
            p.style.left = (x - 10) + 'px';
            p.style.top = (y - 20) + 'px';
            
            document.body.appendChild(p);
            
            // Remove do HTML após a animação acabar para não travar o PC
            setTimeout(() => p.remove(), 700);
        }
    </script>
</body>
</html>
