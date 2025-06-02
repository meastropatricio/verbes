<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>100 Verbes FranÃ§ais-Espagnol</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            overflow: hidden;
            height: 100vh;
        }

        .presentation-container {
            display: flex;
            flex-direction: column;
            height: 100vh;
            position: relative;
        }

        .slide {
            display: none;
            flex: 1;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 40px;
            background: white;
            margin: 20px;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            position: relative;
            overflow: hidden;
        }

        .slide.active {
            display: flex;
            flex-direction: column;
            animation: slideIn 0.5s ease-in-out;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateX(100px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        .slide-number {
            position: absolute;
            top: 20px;
            right: 20px;
            background: rgba(102, 126, 234, 0.1);
            padding: 10px 15px;
            border-radius: 15px;
            font-weight: bold;
            color: #667eea;
        }

        .verb-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 30px;
            max-width: 800px;
        }

        .verb-image {
            width: 200px;
            height: 200px;
            background: linear-gradient(45deg, #ff9a9e, #fecfef);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 80px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
        }

        .verb-image:hover {
            transform: scale(1.1);
        }

        .french-verb {
            font-size: 3.5em;
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 10px;
            text-transform: capitalize;
        }

        .spanish-verb {
            font-size: 2.5em;
            color: #e74c3c;
            font-weight: 600;
            font-style: italic;
        }

        .flag-container {
            display: flex;
            gap: 20px;
            margin-top: 20px;
        }

        .flag {
            width: 40px;
            height: 30px;
            border-radius: 5px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .flag.french {
            background: linear-gradient(to right, #0055a4 33%, white 33%, white 66%, #ef4135 66%);
        }

        .flag.spanish {
            background: linear-gradient(to bottom, #aa151b 25%, #f1bf00 25%, #f1bf00 75%, #aa151b 75%);
        }

        .controls {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 15px;
            z-index: 1000;
        }

        .btn {
            padding: 15px 25px;
            border: none;
            border-radius: 25px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .btn-prev {
            background: linear-gradient(135deg, #ff6b6b, #ee5a24);
            color: white;
        }

        .btn-next {
            background: linear-gradient(135deg, #4ecdc4, #44a08d);
            color: white;
        }

        .btn-play {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
        }

        .btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }

        .progress-bar {
            position: fixed;
            top: 0;
            left: 0;
            height: 4px;
            background: linear-gradient(to right, #667eea, #764ba2);
            transition: width 0.3s ease;
            z-index: 1000;
        }

        .title-slide {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        .title-slide h1 {
            font-size: 4em;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .title-slide p {
            font-size: 1.5em;
            opacity: 0.9;
        }
    </style>
</head>
<body>
    <div class="progress-bar" id="progressBar"></div>
    
    <div class="presentation-container">
        <!-- Slide de titre -->
        <div class="slide active title-slide">
            <h1>ð«ð· âï¸ ðªð¸</h1>
            <h1>100 Verbes</h1>
            <p>FranÃ§ais â Espagnol</p>
            <p style="margin-top: 20px; font-size: 1.2em;">Vocabulaire essentiel pour apprendre l'espagnol</p>
        </div>

        <!-- Slides des verbes -->
    </div>

    <div class="controls">
        <button class="btn btn-prev" id="prevBtn" onclick="previousSlide()">â¬ï¸ PrÃ©cÃ©dent</button>
        <button class="btn btn-play" id="playBtn" onclick="toggleAutoplay()">â¶ï¸ Auto</button>
        <button class="btn btn-next" id="nextBtn" onclick="nextSlide()">Suivant â¡ï¸</button>
    </div>

    <script>
        const verbs = [
            {french: "accepter", spanish: "aceptar", emoji: "â"},
            {french: "acheter", spanish: "comprar", emoji: "ð"},
            {french: "agir", spanish: "actuar", emoji: "ð­"},
            {french: "aimer", spanish: "gustar", emoji: "â¤ï¸"},
            {french: "aller", spanish: "ir", emoji: "ð¶"},
            {french: "apporter", spanish: "traer", emoji: "ð¦"},
            {french: "apprendre", spanish: "aprender", emoji: "ð"},
            {french: "arriver", spanish: "llegar", emoji: "ð"},
            {french: "avoir", spanish: "tener", emoji: "ð¤²"},
            {french: "avoir besoin", spanish: "necesitar", emoji: "ð"},
            {french: "boire", spanish: "beber", emoji: "ð¥¤"},
            {french: "bouger", spanish: "mover", emoji: "ð"},
            {french: "changer", spanish: "cambiar", emoji: "ð"},
            {french: "chanter", spanish: "cantar", emoji: "ð¤"},
            {french: "chercher", spanish: "buscar", emoji: "ð"},
            {french: "choisir", spanish: "elegir", emoji: "ð"},
            {french: "commencer", spanish: "empezar", emoji: "ð"},
            {french: "connaÃ®tre", spanish: "conocer", emoji: "ð¤"},
            {french: "croire", spanish: "creer", emoji: "ð­"},
            {french: "cuisiner", spanish: "cocinar", emoji: "ð¨âð³"},
            {french: "danser", spanish: "bailar", emoji: "ð"},
            {french: "dÃ©cider", spanish: "decidir", emoji: "âï¸"},
            {french: "dÃ©fendre", spanish: "defender", emoji: "ð¡ï¸"},
            {french: "demander", spanish: "pedir", emoji: "ð"},
            {french: "descendre", spanish: "bajar", emoji: "â¬ï¸"},
            {french: "devoir", spanish: "deber", emoji: "â ï¸"},
            {french: "dire", spanish: "decir", emoji: "ð¬"},
            {french: "donner", spanish: "dar", emoji: "ð"},
            {french: "dormir", spanish: "dormir", emoji: "ð´"},
            {french: "douter", spanish: "dudar", emoji: "ð¤"},
            {french: "Ã©couter", spanish: "escuchar", emoji: "ð"},
            {french: "Ã©crire", spanish: "escribir", emoji: "âï¸"},
            {french: "entendre", spanish: "oir", emoji: "ð"},
            {french: "entrer", spanish: "entrar", emoji: "ðª"},
            {french: "espÃ©rer", spanish: "esperar", emoji: "ð"},
            {french: "essayer", spanish: "intentar", emoji: "ðª"},
            {french: "Ãªtre", spanish: "ser/estar", emoji: "ð"},
            {french: "Ã©tudier", spanish: "estudiar", emoji: "ð"},
            {french: "faire", spanish: "hacer", emoji: "ð¨"},
            {french: "guider", spanish: "guiar", emoji: "ð§­"},
            {french: "ignorer", spanish: "ignorar", emoji: "ð"},
            {french: "interdire", spanish: "prohibir", emoji: "ð«"},
            {french: "inviter", spanish: "invitar", emoji: "ð"},
            {french: "jouer", spanish: "jugar", emoji: "ð®"},
            {french: "laisser", spanish: "dejar", emoji: "ð"},
            {french: "lire", spanish: "leer", emoji: "ð"},
            {french: "manger", spanish: "comer", emoji: "ð½ï¸"},
            {french: "marcher", spanish: "andar", emoji: "ð¶"},
            {french: "mentir", spanish: "mentir", emoji: "ð¤¥"},
            {french: "mettre", spanish: "poner", emoji: "ð"},
            {french: "mourir", spanish: "morir", emoji: "ð"},
            {french: "nager", spanish: "nadar", emoji: "ð"},
            {french: "nettoyer", spanish: "limpiar", emoji: "ð§½"},
            {french: "obtenir", spanish: "obtener", emoji: "ð"},
            {french: "oublier", spanish: "olvidar", emoji: "ð¤¯"},
            {french: "ouvrir", spanish: "abrir", emoji: "ð"},
            {french: "parler", spanish: "hablar", emoji: "ð¬"},
            {french: "partir", spanish: "partir", emoji: "ð§³"},
            {french: "payer", spanish: "pagar", emoji: "ð³"},
            {french: "penser", spanish: "pensar", emoji: "ð§ "},
            {french: "pleurer", spanish: "llorar", emoji: "ð¢"},
            {french: "pleuvoir", spanish: "llover", emoji: "ð§ï¸"},
            {french: "porter", spanish: "llevar", emoji: "ð"},
            {french: "pouvoir", spanish: "poder", emoji: "ðª"},
            {french: "prÃ©fÃ©rer", spanish: "preferir", emoji: "â­"},
            {french: "prendre", spanish: "coger", emoji: "â"},
            {french: "prÃ©senter", spanish: "presentar", emoji: "ð"},
            {french: "produire", spanish: "producir", emoji: "ð­"},
            {french: "raconter", spanish: "contar", emoji: "ð"},
            {french: "refuser", spanish: "negar", emoji: "â"},
            {french: "regarder", spanish: "mirar", emoji: "ð"},
            {french: "reposer", spanish: "descansar", emoji: "ð´"},
            {french: "rÃ©unir", spanish: "reunir", emoji: "ð¥"},
            {french: "rÃ©ussir", spanish: "conseguir", emoji: "â"},
            {french: "rÃ©veiller", spanish: "despertar", emoji: "â°"},
            {french: "revenir", spanish: "volver", emoji: "ð"},
            {french: "rÃªver", spanish: "soÃ±ar", emoji: "ð­"},
            {french: "rire", spanish: "reÃ­r", emoji: "ð"},
            {french: "s'appeler", spanish: "llamarse", emoji: "ð"},
            {french: "satisfaire", spanish: "satisfacer", emoji: "ð"},
            {french: "savoir", spanish: "saber", emoji: "ð§ "},
            {french: "se lever", spanish: "levantarse", emoji: "ð"},
            {french: "sentir", spanish: "sentir", emoji: "ð"},
            {french: "suivre", spanish: "seguir", emoji: "ð£"},
            {french: "tarder", spanish: "tardar", emoji: "â°"},
            {french: "tomber", spanish: "caer", emoji: "ð"},
            {french: "toucher", spanish: "tocar", emoji: "ð"},
            {french: "travailler", spanish: "trabajar", emoji: "ð¼"},
            {french: "utiliser", spanish: "usar", emoji: "ð§"},
            {french: "valoir", spanish: "valer", emoji: "ð"},
            {french: "venir", spanish: "venir", emoji: "â¡ï¸"},
            {french: "vivre", spanish: "vivir", emoji: "ð±"},
            {french: "voir", spanish: "ver", emoji: "ðï¸"},
            {french: "vouloir", spanish: "querer", emoji: "ð"},
            {french: "voyager", spanish: "viajar", emoji: "âï¸"}
        ];

        let currentSlide = 0;
        let isAutoplay = false;
        let autoplayInterval;

        // CrÃ©er les slides
        function createSlides() {
            const container = document.querySelector('.presentation-container');
            
            verbs.forEach((verb, index) => {
                const slide = document.createElement('div');
                slide.className = 'slide';
                slide.innerHTML = `
                    <div class="slide-number">${index + 2}/101</div>
                    <div class="verb-container">
                        <div class="verb-image">${verb.emoji}</div>
                        <div class="french-verb">${verb.french}</div>
                        <div class="spanish-verb">${verb.spanish}</div>
                        <div class="flag-container">
                            <div class="flag french"></div>
                            <div class="flag spanish"></div>
                        </div>
                    </div>
                `;
                container.appendChild(slide);
            });
        }

        function updateSlide() {
            const slides = document.querySelectorAll('.slide');
            const totalSlides = slides.length;
            
            slides.forEach((slide, index) => {
                slide.classList.toggle('active', index === currentSlide);
            });

            // Mettre Ã  jour la barre de progression
            const progress = (currentSlide / (totalSlides - 1)) * 100;
            document.getElementById('progressBar').style.width = progress + '%';

            // Mettre Ã  jour les boutons
            document.getElementById('prevBtn').disabled = currentSlide === 0;
            document.getElementById('nextBtn').disabled = currentSlide === totalSlides - 1;
        }

        function nextSlide() {
            const totalSlides = document.querySelectorAll('.slide').length;
            if (currentSlide < totalSlides - 1) {
                currentSlide++;
                updateSlide();
            }
        }

        function previousSlide() {
            if (currentSlide > 0) {
                currentSlide--;
                updateSlide();
            }
        }

        function toggleAutoplay() {
            const playBtn = document.getElementById('playBtn');
            
            if (isAutoplay) {
                clearInterval(autoplayInterval);
                isAutoplay = false;
                playBtn.innerHTML = 'â¶ï¸ Auto';
                playBtn.style.background = 'linear-gradient(135deg, #667eea, #764ba2)';
            } else {
                isAutoplay = true;
                playBtn.innerHTML = 'â¸ï¸ Pause';
                playBtn.style.background = 'linear-gradient(135deg, #ff6b6b, #ee5a24)';
                
                autoplayInterval = setInterval(() => {
                    const totalSlides = document.querySelectorAll('.slide').length;
                    if (currentSlide < totalSlides - 1) {
                        nextSlide();
                    } else {
                        toggleAutoplay(); // ArrÃªter Ã  la fin
                    }
                }, 3000);
            }
        }

        // Navigation au clavier
        document.addEventListener('keydown', (e) => {
            switch(e.key) {
                case 'ArrowRight':
                case ' ':
                    nextSlide();
                    break;
                case 'ArrowLeft':
                    previousSlide();
                    break;
                case 'Home':
                    currentSlide = 0;
                    updateSlide();
                    break;
                case 'End':
                    currentSlide = document.querySelectorAll('.slide').length - 1;
                    updateSlide();
                    break;
            }
        });

        // Initialisation
        createSlides();
        updateSlide();
    </script>
</body>
</html>

