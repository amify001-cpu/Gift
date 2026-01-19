<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🎂 A Special Birthday & Question</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            cursor: none !important;
        }

        body {
            font-family: 'Georgia', serif;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
            transition: background 1s ease;
        }

        /* Custom Heart Cursor */
        .cursor-heart {
            position: fixed;
            width: 20px;
            height: 20px;
            pointer-events: none;
            z-index: 10000;
            transition: transform 0.1s ease;
        }

        .cursor-trail {
            position: fixed;
            width: 12px;
            height: 12px;
            pointer-events: none;
            z-index: 9999;
            opacity: 0;
            animation: trailFade 0.6s ease-out forwards;
        }

        @keyframes trailFade {
            0% { opacity: 1; transform: scale(1); }
            100% { opacity: 0; transform: scale(0.3); }
        }

        /* Floating background elements */
        .float-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        .float-emoji {
            position: absolute;
            font-size: 30px;
            animation: float 6s infinite ease-in-out;
            opacity: 0.3;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(0deg); opacity: 0.3; }
            50% { transform: translateY(-50px) rotate(10deg); opacity: 0.6; }
        }

        .container {
            background: white;
            border-radius: 30px;
            padding: 60px 50px;
            max-width: 650px;
            width: 90%;
            text-align: center;
            box-shadow: 0 30px 80px rgba(0, 0, 0, 0.3);
            position: relative;
            z-index: 10;
            animation: slideIn 0.8s ease-out;
        }

        @keyframes slideIn {
            from { transform: scale(0.8) translateY(50px); opacity: 0; }
            to { transform: scale(1) translateY(0); opacity: 1; }
        }

        .stage {
            display: none;
        }

        .stage.active {
            display: block;
            animation: fadeIn 0.6s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        h1 {
            font-size: 2.5em;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }

        .emoji {
            font-size: 80px;
            margin: 20px 0;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }

        p {
            font-size: 1.3em;
            color: #555;
            margin: 25px 0;
            line-height: 1.6;
        }

        .btn-group {
            display: flex;
            gap: 20px;
            justify-content: center;
            margin-top: 40px;
            flex-wrap: wrap;
        }

        button {
            padding: 15px 40px;
            font-size: 1.2em;
            font-weight: bold;
            border: none;
            border-radius: 50px;
            cursor: none !important;
            transition: all 0.3s ease;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.2);
            font-family: 'Georgia', serif;
        }

        .btn-yes {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
        }

        .btn-yes:hover {
            transform: scale(1.1) rotate(2deg);
            box-shadow: 0 8px 30px rgba(245, 87, 108, 0.5);
        }

        .btn-no {
            background: linear-gradient(135deg, #c2c2c2 0%, #8e8e8e 100%);
            color: white;
        }

        .btn-no:hover {
            transform: scale(0.95);
        }

        .btn-no-tricky {
            position: fixed;
            transition: all 0.3s ease;
        }

        .progress {
            margin: 30px 0 10px 0;
            font-size: 0.9em;
            color: #999;
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: #e0e0e0;
            border-radius: 10px;
            overflow: hidden;
            margin: 10px 0 30px 0;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
            transition: width 0.5s ease;
        }

        /* Birthday Stage Unique Styles */
        .birthday-stage-1 { background: linear-gradient(135deg, #FFB6C1 0%, #FFC0CB 100%); }
        .birthday-stage-2 { background: linear-gradient(135deg, #87CEEB 0%, #B0E0E6 100%); }
        .birthday-stage-3 { background: linear-gradient(135deg, #DDA0DD 0%, #E6E6FA 100%); }
        
        .birthday-stage-1 h1 { color: #C71585; }
        .birthday-stage-2 h1 { color: #1E90FF; }
        .birthday-stage-3 h1 { color: #9370DB; }

        /* Celebration Screen */
        .celebration {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, #ffd89b 0%, #19547b 100%);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            animation: fadeInBright 2s ease-in;
        }

        @keyframes fadeInBright {
            0% { opacity: 0; filter: brightness(0.3); }
            50% { opacity: 0.7; filter: brightness(1.5); }
            100% { opacity: 1; filter: brightness(1); }
        }

        .celebration.active {
            display: flex;
        }

        .celebration h1 {
            font-size: 4em;
            color: white;
            text-shadow: 3px 3px 10px rgba(0, 0, 0, 0.3);
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        .celebration .emoji {
            font-size: 150px;
            animation: spin 3s linear infinite;
        }

        @keyframes spin {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        .firework {
            position: absolute;
            width: 5px;
            height: 5px;
            border-radius: 50%;
            animation: explode 1s ease-out infinite;
        }

        @keyframes explode {
            0% { transform: scale(1) translate(0, 0); opacity: 1; }
            100% { transform: scale(20) translate(var(--x), var(--y)); opacity: 0; }
        }

        @media (max-width: 600px) {
            .container {
                padding: 40px 30px;
                margin: 20px;
            }
            h1 { font-size: 2em; }
            p { font-size: 1.1em; }
            button { padding: 12px 30px; font-size: 1em; }
        }
    </style>
</head>
<body style="background: linear-gradient(135deg, #FFB6C1 0%, #FFC0CB 100%);">
    
    <!-- Custom Cursor -->
    <div class="cursor-heart" id="cursorHeart">❤️</div>

    <!-- Floating background -->
    <div class="float-bg" id="floatBg"></div>

    <!-- Main container -->
    <div class="container" id="mainContainer">

        <!-- BIRTHDAY STAGE 1 -->
        <div class="stage active" id="stage0">
            <div class="emoji">🎂</div>
            <h1 style="color: #C71585;">Happy Birthday, Beautiful!</h1>
            <p>Today is YOUR day! A day to celebrate the amazing person you are. 🎉</p>
            <p>You light up every room you enter, and I'm so grateful to know you!</p>
            <div class="btn-group">
                <button class="btn-yes" onclick="nextStage(1)">Thank you! 💖</button>
            </div>
        </div>

        <!-- BIRTHDAY STAGE 2 -->
        <div class="stage" id="stage1">
            <div class="emoji">🎈</div>
            <h1 style="color: #1E90FF;">Your Special Day</h1>
            <p>Every year, you become even more incredible...</p>
            <p>More beautiful, more kind, more everything! ✨</p>
            <p>Do you know how much joy you bring to my life?</p>
            <div class="btn-group">
                <button class="btn-yes" onclick="nextStage(2)">I hope so! 😊</button>
                <button class="btn-no" onclick="noResponse(0)">Tell me more...</button>
            </div>
        </div>

        <!-- BIRTHDAY STAGE 3 -->
        <div class="stage" id="stage2">
            <div class="emoji">🎁</div>
            <h1 style="color: #9370DB;">A Birthday Surprise</h1>
            <p>I have something very special planned for you today...</p>
            <p>Something that comes straight from my heart. 💝</p>
            <p>Are you ready for your birthday surprise?</p>
            <div class="btn-group">
                <button class="btn-yes" onclick="transitionToRomantic()">Yes! Show me! 🎊</button>
                <button class="btn-no" onclick="noResponse(1)">I'm nervous...</button>
            </div>
        </div>

        <!-- LOVE STAGE 1 -->
        <div class="stage" id="stage3">
            <div class="progress">Step 1 of 5</div>
            <div class="progress-bar"><div class="progress-fill" style="width: 20%;"></div></div>
            <div class="emoji">💝</div>
            <h1 style="color: #764ba2;">A Journey of Love</h1>
            <p>From the moment I met you, I knew you were special...</p>
            <p>Every day with you has been a beautiful adventure. 🌹</p>
            <p>Shall we walk down memory lane together?</p>
            <div class="btn-group">
                <button class="btn-yes" onclick="nextStage(4)">Yes, let's go! 💕</button>
                <button class="btn-no" onclick="noResponse(2)">Not sure...</button>
            </div>
        </div>

        <!-- LOVE STAGE 2 -->
        <div class="stage" id="stage4">
            <div class="progress">Step 2 of 5</div>
            <div class="progress-bar"><div class="progress-fill" style="width: 40%;"></div></div>
            <div class="emoji">🌹</div>
            <h1 style="color: #764ba2;">Our Beautiful Memories</h1>
            <p>Do you remember all the laughter we've shared?</p>
            <p>Every smile, every moment that took my breath away... 🥰</p>
            <p>Those memories are treasures I'll cherish forever.</p>
            <div class="btn-group">
                <button class="btn-yes" onclick="nextStage(5)">I remember! ❤️</button>
                <button class="btn-no" onclick="noResponse(3)">Remind me...</button>
            </div>
        </div>

        <!-- LOVE STAGE 3 -->
        <div class="stage" id="stage5">
            <div class="progress">Step 3 of 5</div>
            <div class="progress-bar"><div class="progress-fill" style="width: 60%;"></div></div>
            <div class="emoji">💞</div>
            <h1 style="color: #764ba2;">You're My Everything</h1>
            <p>You make every day brighter, every moment sweeter...</p>
            <p>My heart beats for you in ways I never knew possible. 💗</p>
            <p>Can you feel how much you mean to me?</p>
            <div class="btn-group">
                <button class="btn-yes" onclick="nextStage(6)">Yes, I feel it! 💕</button>
                <button class="btn-no" onclick="noResponse(4)">Show me more...</button>
            </div>
        </div>

        <!-- LOVE STAGE 4 -->
        <div class="stage" id="stage6">
            <div class="progress">Step 4 of 5</div>
            <div class="progress-bar"><div class="progress-fill" style="width: 80%;"></div></div>
            <div class="emoji">👑</div>
            <h1 style="color: #764ba2;">Our Forever</h1>
            <p>I dream of a lifetime of adventures with you...</p>
            <p>Waking up together, building dreams, growing old side by side... 🌟</p>
            <p>Does that future sound beautiful to you?</p>
            <div class="btn-group">
                <button class="btn-yes" onclick="nextStage(7)">Yes, it does! 💍</button>
                <button class="btn-no" onclick="noResponse(5)">I'm thinking...</button>
            </div>
        </div>

        <!-- THE BIG QUESTION -->
        <div class="stage" id="stage7">
            <div class="progress">Step 5 of 5 — The Moment! 💍</div>
            <div class="progress-bar"><div class="progress-fill" style="width: 100%;"></div></div>
            <div class="emoji">💍</div>
            <h1 style="color: #764ba2;">Will You Marry Me?</h1>
            <p>You are my forever, my always, my everything...</p>
            <p>Will you make me the happiest person alive and marry me? 💖</p>
            <div class="btn-group">
                <button class="btn-yes" onclick="celebrate()" style="font-size: 1.5em; padding: 20px 50px;">YES! I WILL! 💍</button>
                <button class="btn-no btn-no-tricky" id="trickyNo" onmouseover="runAway()" onclick="runAway()">No</button>
            </div>
        </div>

    </div>

    <!-- Celebration Screen -->
    <div class="celebration" id="celebration">
        <div class="emoji">💍</div>
        <h1>SHE SAID YES! 🎉</h1>
        <p style="font-size: 2em; color: white; margin-top: 20px;">Forever starts now! 💕✨</p>
        <div id="fireworks"></div>
    </div>

    <script>
        // Custom Heart Cursor Trail
        const cursorHeart = document.getElementById('cursorHeart');
        let mouseX = 0, mouseY = 0;
        let cursorX = 0, cursorY = 0;

        document.addEventListener('mousemove', (e) => {
            mouseX = e.clientX;
            mouseY = e.clientY;
            
            // Create trail hearts
            if (Math.random() > 0.7) {
                createTrailHeart(e.clientX, e.clientY);
            }
        });

        function createTrailHeart(x, y) {
            const trail = document.createElement('div');
            trail.className = 'cursor-trail';
            trail.textContent = '❤️';
            trail.style.left = x + 'px';
            trail.style.top = y + 'px';
            trail.style.fontSize = (Math.random() * 10 + 8) + 'px';
            document.body.appendChild(trail);
            setTimeout(() => trail.remove(), 600);
        }

        function animateCursor() {
            cursorX += (mouseX - cursorX) * 0.2;
            cursorY += (mouseY - cursorY) * 0.2;
            cursorHeart.style.left = cursorX + 'px';
            cursorHeart.style.top = cursorY + 'px';
            requestAnimationFrame(animateCursor);
        }
        animateCursor();

        // Generate floating emojis
        function createFloatingEmojis(emoji) {
            const floatBg = document.getElementById('floatBg');
            floatBg.innerHTML = '';
            for (let i = 0; i < 15; i++) {
                const float = document.createElement('div');
                float.className = 'float-emoji';
                float.textContent = emoji;
                float.style.left = Math.random() * 100 + '%';
                float.style.top = Math.random() * 100 + '%';
                float.style.animationDelay = Math.random() * 3 + 's';
                floatBg.appendChild(float);
            }
        }
        createFloatingEmojis('🎈');

        let currentStage = 0;
        const backgrounds = {
            0: 'linear-gradient(135deg, #FFB6C1 0%, #FFC0CB 100%)',
            1: 'linear-gradient(135deg, #87CEEB 0%, #B0E0E6 100%)',
            2: 'linear-gradient(135deg, #DDA0DD 0%, #E6E6FA 100%)',
            3: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)'
        };

        function nextStage(stage) {
            document.getElementById('stage' + currentStage).classList.remove('active');
            currentStage = stage;
            document.getElementById('stage' + stage).classList.add('active');
            
            // Change background for birthday stages
            if (stage <= 2) {
                document.body.style.background = backgrounds[stage];
            }
        }

        function noResponse(type) {
            const messages = [
                "You bring endless joy! Let me show you more... 💕",
                "Don't be nervous! It's something wonderful, I promise! 🥰",
                "Trust me, you're going to love this... 💖",
                "Every single beautiful moment with you! 🥰",
                "Let me show you just how much... 💕",
                "Think about all the amazing adventures ahead! 🌟"
            ];
            alert(messages[type] || "Click YES to continue this journey! 💕");
        }

        function transitionToRomantic() {
            document.body.style.background = backgrounds[3];
            createFloatingEmojis('💕');
            nextStage(3);
        }

        function runAway() {
            const noBtn = document.getElementById('trickyNo');
            const maxX = window.innerWidth - 200;
            const maxY = window.innerHeight - 100;
            noBtn.style.left = Math.random() * maxX + 'px';
            noBtn.style.top = Math.random() * maxY + 'px';
        }

        function celebrate() {
            document.getElementById('mainContainer').style.display = 'none';
            document.getElementById('celebration').classList.add('active');
            createFireworks();
        }

        function createFireworks() {
            const fireworksContainer = document.getElementById('fireworks');
            const colors = ['#ff6b6b', '#feca57', '#48dbfb', '#ff9ff3', '#54a0ff', '#5f27cd'];

            setInterval(() => {
                for (let i = 0; i < 10; i++) {
                    const firework = document.createElement('div');
                    firework.className = 'firework';
                    firework.style.background = colors[Math.floor(Math.random() * colors.length)];
                    firework.style.left = Math.random() * 100 + '%';
                    firework.style.top = Math.random() * 100 + '%';
                    firework.style.setProperty('--x', (Math.random() - 0.5) * 200 + 'px');
                    firework.style.setProperty('--y', (Math.random() - 0.5) * 200 + 'px');
                    firework.style.animationDelay = Math.random() * 0.5 + 's';
                    fireworksContainer.appendChild(firework);
                    setTimeout(() => firework.remove(), 1000);
                }
            }, 500);
        }
    </script>
</body>
</html>
