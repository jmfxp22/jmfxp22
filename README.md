<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Surpresa Interativa</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            color: white;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-align: center;
            padding: 20px;
            transition: background 0.5s ease;
            overflow-x: hidden;
        }
        
        .container {
            max-width: 800px;
            width: 100%;
            padding: 40px;
            background-color: rgba(255, 255, 255, 0.1);
            border-radius: 25px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(15px);
            margin: 20px 0;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        h1 {
            font-size: 3rem;
            margin-bottom: 25px;
            text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.3);
            background: linear-gradient(to right, #ff8a00, #da1b60);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        p {
            font-size: 1.3rem;
            line-height: 1.7;
            margin-bottom: 25px;
        }
        
        .btn {
            background: linear-gradient(to right, #ff8a00, #da1b60);
            color: white;
            border: none;
            padding: 18px 50px;
            font-size: 1.3rem;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
            margin: 15px;
            font-weight: bold;
            letter-spacing: 1px;
            position: relative;
            overflow: hidden;
        }
        
        .btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 25px rgba(0, 0, 0, 0.4);
        }
        
        .btn:active {
            transform: translateY(2px);
        }
        
        .btn::after {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: 0.5s;
        }
        
        .btn:hover::after {
            left: 100%;
        }
        
        .hidden {
            display: none;
        }
        
        .step {
            animation: fadeIn 0.8s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .image-container {
            margin: 40px 0;
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.4);
            transform: perspective(1000px) rotateX(5deg);
            transition: transform 0.5s ease;
        }
        
        .image-container:hover {
            transform: perspective(1000px) rotateX(0);
        }
        
        .image-container img {
            max-width: 100%;
            height: auto;
            display: block;
            transition: transform 0.5s ease;
        }
        
        .image-container:hover img {
            transform: scale(1.05);
        }
        
        .black-section {
            background-color: #121212;
            color: white;
            padding: 60px 30px;
            width: 100%;
            margin-top: 40px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            border: 2px solid #333;
        }
        
        .final-message {
            background: linear-gradient(135deg, #ff6b6b 0%, #feca57 100%);
            color: #222;
            padding: 50px;
            border-radius: 25px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
            max-width: 700px;
            margin: 0 auto;
            border: 3px solid rgba(255, 255, 255, 0.3);
        }
        
        .final-message h2 {
            font-size: 2.5rem;
            margin-bottom: 25px;
            color: #8a2be2;
            text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.2);
        }
        
        .heart {
            color: #ff4757;
            font-size: 2.5rem;
            margin: 0 8px;
            animation: pulse 1.5s infinite;
            display: inline-block;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.3); }
            100% { transform: scale(1); }
        }
        
        .arrow {
            font-size: 2.5rem;
            margin: 15px 0;
            animation: bounce 2s infinite;
        }
        
        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-15px); }
            60% { transform: translateY(-7px); }
        }
        
        .emoji {
            font-size: 2rem;
            margin: 0 5px;
            animation: spin 4s infinite linear;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        .loading {
            display: inline-block;
            width: 30px;
            height: 30px;
            border: 4px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top-color: #fff;
            animation: spin 1s ease-in-out infinite;
            margin: 0 10px;
        }
        
        .funny-text {
            font-style: italic;
            color: #ffcc00;
            font-weight: bold;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
        }
        
        .highlight {
            background: linear-gradient(transparent 60%, #ffcc00 40%);
            padding: 0 5px;
            font-weight: bold;
        }
        
        .floating {
            animation: float 6s ease-in-out infinite;
        }
        
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
            100% { transform: translateY(0px); }
        }
        
        .confetti {
            position: fixed;
            width: 15px;
            height: 15px;
            background-color: #f00;
            opacity: 0;
            animation: confetti-fall 5s linear forwards;
            z-index: 1000;
        }
        
        @keyframes confetti-fall {
            0% {
                transform: translateY(-100px) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }
        
        @media (max-width: 768px) {
            h1 {
                font-size: 2.2rem;
            }
            
            p {
                font-size: 1.1rem;
            }
            
            .container {
                padding: 25px;
            }
            
            .btn {
                padding: 15px 35px;
                font-size: 1.1rem;
            }
        }
    </style>
</head>
<body>
    <!-- Etapa 1: Clique Aqui -->
    <div id="step1" class="container step">
        <h1>Ei, Você Aí!</h1>
        <p>Prepare-se para uma experiência única que vai mudar sua vida! (Ou não)</p>
        <div class="arrow floating">👇</div>
        <button class="btn" onclick="showStep(2)">Clique Aqui</button>
        <p class="funny-text">Prometo que não é vírus!</p>
    </div>
    
    <!-- Etapa 2: Clique Novamente -->
    <div id="step2" class="container step hidden">
        <h1>Eita!</h1>
        <p>Parece que meus dados não carregaram <span class="loading"></span></p>
        <p class="funny-text">Ou será que você clicou errado? <span class="emoji">🤔</span></p>
        <button class="btn" onclick="showStep(3)">Clique Novamente</button>
    </div>
    
    <!-- Etapa 3: Imagem -->
    <div id="step3" class="container step hidden">
        <h1>Carregando...</h1>
        <p>Estamos quase lá! Só mais um pouquinho de paciência.</p>
        <p class="funny-text">Ou não, porque isso pode demorar <span class="emoji">😅</span></p>
        <div class="image-container">
            <img src="https://cdn.discordapp.com/attachments/1414287333997674516/1441356804318826586/3d870be629354eb6f9594daa9afde96f.jpg" alt="Imagem misteriosa">
        </div>
        <p>Role para baixo para continuar</p>
        <div class="arrow">👇</div>
    </div>
    
    <!-- Etapa 4: Seção Preta -->
    <div id="step4" class="black-section step hidden">
        <h1>Sai Daqui! <span class="emoji">😠</span></h1>
        <p>Eu já falei que meus dados ainda não carregaram!</p>
        <p class="funny-text">Você é teimoso(a) mesmo, hein? <span class="emoji">🙄</span></p>
        <button class="btn" onclick="showStep(5)">Voltar para Home</button>
    </div>
    
    <!-- Etapa 5: Mensagem Final -->
    <div id="step5" class="container step hidden">
        <div class="final-message">
            <h2>Mensagem Especial! <span class="heart">❤️</span></h2>
            <p>Olha, vim através deste site dizer que você é um amigo muito especial pra mim.</p>
            <p>Em meio às brincadeiras pesadas, xingamentos e aquelas <span class="highlight">piadas sem graça</span> que você conta...</p>
            <p>Eu realmente gosto da sua companhia! <span class="emoji">😊</span></p>
            <p>Obrigado por aturar minhas <span class="highlight">manias irritantes</span> e ainda assim me considerar um amigo.</p>
            <p>Você é <span class="highlight">ÚNICO(A)</span>... no sentido literal mesmo, não tem outro igual!</p>
            <p>Continue sendo essa pessoa <span class="highlight">especialmente estranha</span> que você é!</p>
            <p class="funny-text">Agora vai lá e para de ficar clicando em coisas na internet! <span class="emoji">🤪</span></p>
        </div>
        <button class="btn" onclick="showStep(1)">Recomeçar</button>
    </div>

    <script>
        function showStep(stepNumber) {
            // Esconde todas as etapas
            document.querySelectorAll('.step').forEach(step => {
                step.classList.add('hidden');
            });
            
            // Mostra a etapa selecionada
            document.getElementById(`step${stepNumber}`).classList.remove('hidden');
            
            // Rola para o topo da página
            window.scrollTo(0, 0);
            
            // Muda o fundo para a etapa 4
            if (stepNumber === 4) {
                document.body.style.background = '#121212';
            } else {
                document.body.style.background = 'linear-gradient(135deg, #6a11cb 0%, #2575fc 100%)';
            }
            
            // Cria confetti na última etapa
            if (stepNumber === 5) {
                createConfetti();
            }
        }
        
        // Adiciona evento de scroll para mostrar a etapa 4 automaticamente
        window.addEventListener('scroll', function() {
            const step3 = document.getElementById('step3');
            const step4 = document.getElementById('step4');
            
            if (!step3.classList.contains('hidden') && 
                window.scrollY + window.innerHeight >= document.body.scrollHeight - 100) {
                showStep(4);
            }
        });
        
        // Função para criar confetti
        function createConfetti() {
            const colors = ['#ff0000', '#00ff00', '#0000ff', '#ffff00', '#ff00ff', '#00ffff'];
            const confettiCount = 150;
            
            for (let i = 0; i < confettiCount; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = Math.random() * 100 + 'vw';
                confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.width = Math.random() * 15 + 5 + 'px';
                confetti.style.height = Math.random() * 15 + 5 + 'px';
                confetti.style.animationDuration = Math.random() * 3 + 2 + 's';
                confetti.style.animationDelay = Math.random() * 2 + 's';
                
                document.body.appendChild(confetti);
                
                // Remove o confetti após a animação
                setTimeout(() => {
                    confetti.remove();
                }, 7000);
            }
        }
        
        // Adiciona efeito de digitação na mensagem final
        document.addEventListener('DOMContentLoaded', function() {
            const finalMessage = document.querySelector('.final-message');
            if (finalMessage) {
                finalMessage.style.opacity = '0';
                setTimeout(() => {
                    finalMessage.style.transition = 'opacity 1.5s ease';
                    finalMessage.style.opacity = '1';
                }, 500);
            }
        });
    </script>
</body>
</html>
