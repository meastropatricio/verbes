<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>100 Verbes Français-Espagnol</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">
    
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; /* Poppins en premier */
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
            gap: 10px; /* Réduit l'espace entre les boutons */
            z-index: 1000;
        }

        .btn {
            padding: 12px 20px; /* Réduit le padding pour des boutons plus petits */
            border: none;
            border-radius: 20px; /* Ajuste le border-radius */
            font-size: 15px; /* Réduit la taille de police */
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            display: flex; /* Pour aligner l'icône et le texte */
            align-items: center;
            gap: 5px; /* Espace entre l'icône et le texte */
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
        <div class="slide active title-slide">
            <h1>🇫🇷 ↔️ 🇪🇸</h1>
            <h1>100 Verbes</h1>
            <p>Français ↔️ Espagnol</p>
            <p style="margin-top: 20px; font-size: 1.2em;">Vocabulaire essentiel pour apprendre l'espagnol</p>
        </div>

        </div>

    <div class="controls">
        <button class="btn btn-prev" id="prevBtn" onclick="previousSlide()"><i class="fas fa-arrow-left"></i> Précédent</button>
        <button class="btn btn-play" id="playBtn" onclick="toggleAutoplay()"><i class="fas fa-play"></i> Auto</button>
        <button class="btn btn-next" id="nextBtn" onclick="nextSlide()">Suivant <i class="fas fa-arrow-right"></i></button>
    </div>

    <script>
        const verbs = [
            {french: "accepter", spanish: "aceptar", emoji: "✅"},
            {french: "acheter", spanish: "comprar", emoji: "🛒"},
            {french: "agir", spanish: "actuar", emoji: "🎬"},
            {french: "aimer", spanish: "gustar", emoji: "❤️"},
            {french: "aller", spanish: "ir", emoji: "🚶"},
            {french: "apporter", spanish: "traer", emoji: "📦"},
            {french: "apprendre", spanish: "aprender", emoji: "📚"},
            {french: "arriver", spanish: "llegar", emoji: "🏁"},
            {french: "avoir", spanish: "tener", emoji: "🤞"},
            {french: "avoir besoin", spanish: "necesitar", emoji: "🆘"},
            {french: "boire", spanish: "beber", emoji: "🥛"},
            {french: "bouger", spanish: "mover", emoji: "💃"},
            {french: "changer", spanish: "cambiar", emoji: "🔄"},
            {french: "chanter", spanish: "cantar", emoji: "🎤"},
            {french: "chercher", spanish: "buscar", emoji: "🔎"},
            {french: "choisir", spanish: "elegir", emoji: "👆"},
            {french: "commencer", spanish: "empezar", emoji: "🏁"},
            {french: "connaître", spanish: "conocer", emoji: "🤝"},
            {french: "croire", spanish: "creer", emoji: "💭"},
            {french: "cuisiner", spanish: "cocinar", emoji: "👨‍🍳"},
            {french: "danser", spanish: "bailar", emoji: "💃"},
            {french: "décider", spanish: "decidir", emoji: "⚖️"},
            {french: "défendre", spanish: "defender", emoji: "🛡️"},
            {french: "demander", spanish: "pedir", emoji: "🙏"},
            {french: "descendre", spanish: "bajar", emoji: "⬇️"},
            {french: "devoir", spanish: "deber", emoji: "⚠️"},
            {french: "dire", spanish: "decir", emoji: "💬"},
            {french: "donner", spanish: "dar", emoji: "🎁"},
            {french: "dormir", spanish: "dormir", emoji: "😴"},
            {french: "douter", spanish: "dudar", emoji: "🤔"},
            {french: "écouter", spanish: "escuchar", emoji: "👂"},
            {french: "écrire", spanish: "escribir", emoji: "✍️"},
            {french: "entendre", spanish: "oir", emoji: "👂"},
            {french: "entrer", spanish: "entrar", emoji: "🚪"},
            {french: "espérer", spanish: "esperar", emoji: "🙏"},
            {french: "essayer", spanish: "intentar", emoji: "💪"},
            {french: "être", spanish: "ser/estar", emoji: "🌟"},
            {french: "étudier", spanish: "estudiar", emoji: "📖"},
            {french: "faire", spanish: "hacer", emoji: "🛠️"},
            {french: "guider", spanish: "guiar", emoji: "🧭"},
            {french: "ignorer", spanish: "ignorar", emoji: "🤷‍♀️"},
            {french: "interdire", spanish: "prohibir", emoji: "🚫"},
            {french: "inviter", spanish: "invitar", emoji: "💌"},
            {french: "jouer", spanish: "jugar", emoji: "🎮"},
            {french: "laisser", spanish: "dejar", emoji: "👋"},
            {french: "lire", spanish: "leer", emoji: "📖"},
            {french: "manger", spanish: "comer", emoji: "🍔"},
            {french: "marcher", spanish: "andar", emoji: "🚶"},
            {french: "mentir", spanish: "mentir", emoji: "🤥"},
            {french: "mettre", spanish: "poner", emoji: "📝"},
            {french: "mourir", spanish: "morir", emoji: "💀"},
            {french: "nager", spanish: "nadar", emoji: "🏊‍♀️"},
            {french: "nettoyer", spanish: "limpiar", emoji: "🧼"},
            {french: "obtenir", spanish: "obtener", emoji: "🏆"},
            {french: "oublier", spanish: "olvidar", emoji: "🤷‍♀️"},
            {french: "ouvrir", spanish: "abrir", emoji: "🔓"},
            {french: "parler", spanish: "hablar", emoji: "🗣️"},
            {french: "partir", spanish: "partir", emoji: "🛫"},
            {french: "payer", spanish: "pagar", emoji: "💳"},
            {french: "penser", spanish: "pensar", emoji: "🧠"},
            {french: "pleurer", spanish: "llorar", emoji: "😢"},
            {french: "pleuvoir", spanish: "llover", emoji: "🌧️"},
            {french: "porter", spanish: "llevar", emoji: "🛍️"},
            {french: "pouvoir", spanish: "poder", emoji: "💪"},
            {french: "préférer", spanish: "preferir", emoji: "⭐"},
            {french: "prendre", spanish: "coger", emoji: "🤏"},
            {french: "présenter", spanish: "presentar", emoji: "👋"},
            {french: "produire", spanish: "producir", emoji: "🏭"},
            {french: "raconter", spanish: "contar", emoji: "📖"},
            {french: "refuser", spanish: "negar", emoji: "❌"},
            {french: "regarder", spanish: "mirar", emoji: "👀"},
            {french: "reposer", spanish: "descansar", emoji: "😴"},
            {french: "réunir", spanish: "reunir", emoji: "👥"},
            {french: "réussir", spanish: "conseguir", emoji: "✅"},
            {french: "réveiller", spanish: "despertar", emoji: "⏰"},
            {french: "revenir", spanish: "volver", emoji: "🔄"},
            {french: "rêver", spanish: "soñar", emoji: "💭"},
            {french: "rire", spanish: "reír", emoji: "😂"},
            {french: "s'appeler", spanish: "llamarse", emoji: "📞"},
            {french: "satisfaire", spanish: "satisfacer", emoji: "😊"},
            {french: "savoir", spanish: "saber", emoji: "🧠"},
            {french: "se lever", spanish: "levantarse", emoji: "☀️"},
            {french: "sentir", spanish: "sentir", emoji: "👃"},
            {french: "suivre", spanish: "seguir", emoji: "👣"},
            {french: "tarder", spanish: "tardar", emoji: "⏰"},
            {french: "tomber", spanish: "caer", emoji: "🍂"},
            {french: "toucher", spanish: "tocar", emoji: "👉"},
            {french: "travailler", spanish: "trabajar", emoji: "💼"},
            {french: "utiliser", spanish: "usar", emoji: "⚙️"},
            {french: "valoir", spanish: "valer", emoji: "💎"},
            {french: "venir", spanish: "venir", emoji: "➡️"},
            {french: "vivre", spanish: "vivir", emoji: "🌱"},
            {french: "voir", spanish: "ver", emoji: "👁️"},
            {french: "vouloir", spanish: "querer", emoji: "💖"},
            {french: "voyager", spanish: "viajar", emoji: "✈️"}
        ];

        let currentSlide = 0;
        let isAutoplay = false;
        let autoplayInterval;

        // Créer les slides
        function createSlides() {
            const container = document.querySelector('.presentation-container');
            
            // J'ai mis à jour le numéro de slide pour correspondre à 100 verbes + 1 slide de titre.
            // Le premier slide est le 1/101, le dernier verbe sera le 101/101.
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

            // Mettre à jour la barre de progression
            const progress = (currentSlide / (totalSlides - 1)) * 100;
            document.getElementById('progressBar').style.width = progress + '%';

            // Mettre à jour les boutons
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
                playBtn.innerHTML = '<i class="fas fa-play"></i> Auto'; // Icône Play
                playBtn.style.background = 'linear-gradient(135deg, #667eea, #764ba2)';
            } else {
                isAutoplay = true;
                playBtn.innerHTML = '<i class="fas fa-pause"></i> Pause'; // Icône Pause
                playBtn.style.background = 'linear-gradient(135deg, #ff6b6b, #ee5a24)';
                
                autoplayInterval = setInterval(() => {
                    const totalSlides = document.querySelectorAll('.slide').length;
                    if (currentSlide < totalSlides - 1) {
                        nextSlide();
                    } else {
                        toggleAutoplay(); // Arrêter à la fin
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
