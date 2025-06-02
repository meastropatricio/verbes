<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>100 Verbes Français-Espagnol</title> 
    
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">
    
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">

    <style>
        /* Réinitialisation de base */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            overflow: hidden;
            height: 100vh;
            display: flex;
            flex-direction: column;
        }

        .presentation-container {
            display: flex;
            flex-direction: column;
            flex: 1;
            position: relative;
            justify-content: center;
            align-items: center;
        }

        .slide {
            display: none;
            flex-direction: column;
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
            max-width: 90%;
            max-height: 90%;
        }

        .slide.active {
            display: flex;
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
            z-index: 10;
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

        /* Taille de police réduite pour les verbes français et espagnols */
        .french-verb {
            font-size: 2.8em; /* Réduit d'environ 20% par rapport à 3.5em */
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 10px;
            text-transform: capitalize;
            word-break: break-word; /* Assure que les mots longs peuvent se couper */
            overflow-wrap: break-word; /* Pour les navigateurs modernes */
            padding: 0 10px; /* Ajoute un peu de padding pour les verbes longs */
        }

        .spanish-verb {
            font-size: 2.8em; /* Réduit d'environ 20% par rapport à 3.5em */
            color: #e74c3c;
            font-weight: bold;
            font-style: italic;
            word-break: break-word; /* Assure que les mots longs peuvent se couper */
            overflow-wrap: break-word; /* Pour les navigateurs modernes */
            padding: 0 10px; /* Ajoute un peu de padding pour les verbes longs */
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
            gap: 10px;
            z-index: 1000;
        }

        .btn {
            padding: 12px 20px;
            border: none;
            border-radius: 20px;
            font-size: 15px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            display: flex;
            align-items: center;
            gap: 5px;
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
        
        /* Media queries pour l'adaptation mobile */
        @media (max-width: 768px) {
            .slide {
                padding: 20px;
                margin: 10px;
            }
            .verb-image {
                width: 120px;
                height: 120px;
                font-size: 50px;
            }
            /* Ajustements pour les verbes sur mobile */
            .french-verb {
                font-size: 2em; /* Plus petit pour les écrans plus petits */
            }
            .spanish-verb {
                font-size: 1.5em; /* Plus petit pour les écrans plus petits */
            }
            .title-slide h1 {
                font-size: 3em;
            }
            .title-slide p {
                font-size: 1.2em;
            }
            .btn {
                padding: 10px 15px;
                font-size: 14px;
                border-radius: 15px;
            }
            .controls {
                bottom: 15px;
                gap: 8px;
            }
            .slide-number {
                top: 10px;
                right: 10px;
                padding: 8px 12px;
                font-size: 0.8em;
            }
        }

        @media (max-width: 480px) {
            .verb-image {
                width: 100px;
                height: 100px;
                font-size: 40px;
            }
            /* Ajustements supplémentaires pour les très petits écrans */
            .french-verb {
                font-size: 1.7em;
            }
            .spanish-verb {
                font-size: 1.2em;
            }
            .title-slide h1 {
                font-size: 2.5em;
            }
            .title-slide p {
                font-size: 1em;
            }
            .btn {
                padding: 8px 12px;
                font-size: 12px;
                border-radius: 12px;
            }
            .controls {
                bottom: 10px;
                gap: 5px;
            }
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

        // Créer les slides dynamiquement
        function createSlides() {
            const container = document.querySelector('.presentation-container');
            
            verbs.forEach((verb, index) => {
                const slide = document.createElement('div');
                slide.className = 'slide';
                // Le numéro de slide commence à 2 car le premier slide est le slide de titre (1/101)
                slide.innerHTML = `
                    <div class="slide-number">${index + 2}/${verbs.length + 1}</div>
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

        // Met à jour le slide actuellement affiché
        function updateSlide() {
            const slides = document.querySelectorAll('.slide');
            const totalSlides = slides.length;
            
            slides.forEach((slide, index) => {
                slide.classList.toggle('active', index === currentSlide);
            });

            // Met à jour la barre de progression
            const progress = (currentSlide / (totalSlides - 1)) * 100;
            document.getElementById('progressBar').style.width = progress + '%';

            // Gère l'état des boutons Précédent/Suivant
            document.getElementById('prevBtn').disabled = currentSlide === 0;
            document.getElementById('nextBtn').disabled = currentSlide === totalSlides - 1;
        }

        // Passe au slide suivant
        function nextSlide() {
            const totalSlides = document.querySelectorAll('.slide').length;
            if (currentSlide < totalSlides - 1) {
                currentSlide++;
                updateSlide();
            }
        }

        // Passe au slide précédent
        function previousSlide() {
            if (currentSlide > 0) {
                currentSlide--;
                updateSlide();
            }
        }

        // Active/désactive le mode de lecture automatique
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
                        toggleAutoplay(); // Arrêter à la fin de la présentation
                    }
                }, 3000); // Change de slide toutes les 3 secondes
            }
        }

        // Permet la navigation au clavier
        document.addEventListener('keydown', (e) => {
            switch(e.key) {
                case 'ArrowRight': // Flèche droite
                case ' ': // Barre espace
                    nextSlide();
                    break;
                case 'ArrowLeft': // Flèche gauche
                    previousSlide();
                    break;
                case 'Home': // Touche "Début"
                    currentSlide = 0;
                    updateSlide();
                    break;
                case 'End': // Touche "Fin"
                    currentSlide = document.querySelectorAll('.slide').length - 1;
                    updateSlide();
                    break;
            }
        });

        // Initialisation de la présentation au chargement de la page
        createSlides();
        updateSlide();
    </script>
</body>
</html>
