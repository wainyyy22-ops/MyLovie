# MyLovie
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>For My Lovie 💌</title>
    <style>
        :root {
            --primary-color: #ff4d6d;
            --glass-bg: rgba(255, 255, 255, 0.5);
            --envelope-color: #ffb1c1;
            --envelope-dark: #ff8fa3;
            --wrap-outer: #ffb1c1;
            --wrap-inner: #ffd1dc;
            --ribbon-color: #e63946;
        }

        /* Responsive Viewport Centering */
        * { box-sizing: border-box; }
        
        body, html {
            margin: 0; padding: 0;
            width: 100%; height: 100%;
            display: flex;
            justify-content: center; /* Horizontal Center */
            align-items: center;     /* Vertical Center */
            background: linear-gradient(-45deg, #ffdee9, #fff0f6, #e0c3fc, #b5fffc);
            background-size: 400% 400%;
            animation: gradient 15s ease infinite;
            font-family: 'Comic Sans MS', 'Arial', sans-serif;
            overflow: hidden; 
            position: fixed; /* Prevents scrolling on mobile */
            user-select: none;
            -webkit-tap-highlight-color: transparent;
        }

        @keyframes gradient { 0% { background-position: 0% 50%; } 50% { background-position: 100% 50%; } 100% { background-position: 0% 50%; } }

        .sparkle { position: absolute; background: white; border-radius: 50%; opacity: 0.8; z-index: 2; animation: twinkle var(--duration) ease-in-out infinite; }
        @keyframes twinkle { 0%, 100% { transform: scale(0); opacity: 0; } 50% { transform: scale(1); opacity: 1; } }

        /* The Card Container */
        .screen {
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-align: center;
            width: 90%;
            max-width: 380px; 
            min-height: 480px;
            z-index: 10;
            background: var(--glass-bg);
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px); /* Support for Safari/iOS */
            padding: 30px 20px;
            border-radius: 40px;
            border: 1px solid rgba(255, 255, 255, 0.7);
            box-shadow: 0 20px 45px rgba(0,0,0,0.1);
            position: relative; 
        }

        .active { display: flex; animation: fadeIn 0.4s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: scale(0.9); } to { opacity: 1; transform: scale(1); } }

        h1 { color: var(--primary-color); font-size: 22px; margin: 0 0 20px 0; text-shadow: 1px 1px 4px white; }

        /* Step 1 Centralized Buttons */
        .btn-container { 
            position: relative; 
            display: flex; 
            justify-content: center; 
            align-items: center; 
            width: 100%; 
            height: 250px; 
        }
        
        button { 
            padding: 14px 30px; font-size: 18px; cursor: pointer; border-radius: 50px; border: none; 
            font-weight: bold; box-shadow: 0 10px 20px rgba(0,0,0,0.1); 
            transition: transform 0.1s ease; 
        }

        #yesBtn { background: var(--primary-color); color: white; z-index: 100; position: relative; }
        #noBtn { background: white; color: var(--primary-color); border: 2px solid var(--primary-color); position: absolute; z-index: 50; }

        /* Step 2 Bouquet */
        .bouquet-box {
            position: relative; width: 200px; height: 240px;
            display: flex; justify-content: center; align-items: center;
            margin: 10px 0; animation: float 4s ease-in-out infinite;
        }
        .flower-emoji { font-size: 100px; z-index: 10; position: relative; top: -20px; }
        .wrap-inner { position: absolute; bottom: 40px; width: 90px; height: 120px; background: var(--wrap-inner); clip-path: polygon(10% 0%, 90% 0%, 100% 100%, 0% 100%); z-index: 8; border-top: 2px dashed white; }
        .wrap-outer { position: absolute; bottom: 25px; width: 110px; height: 130px; background: var(--wrap-outer); clip-path: polygon(0% 15%, 100% 15%, 80% 100%, 20% 100%); z-index: 7; }
        .emoji-ribbon { position: absolute; bottom: 55px; width: 100px; height: 14px; background: var(--ribbon-color); border-radius: 20px; z-index: 15; }

        @keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-15px); } }

        /* Step 3 Envelope */
        .envelope-container { position: relative; width: 260px; height: 160px; cursor: pointer; margin: 10px auto; perspective: 1000px; }
        .envelope-back { position: absolute; width: 100%; height: 100%; background: var(--envelope-color); border-radius: 0 0 15px 15px; z-index: 1; }
        .lid { position: absolute; width: 0; height: 0; border-top: 90px solid var(--envelope-dark); border-left: 130px solid transparent; border-right: 130px solid transparent; top: 0; left: 0; transform-origin: top; transition: transform 0.6s ease; z-index: 10; }
        .envelope-front { position: absolute; width: 0; height: 0; border-right: 130px solid var(--envelope-color); border-bottom: 80px solid var(--envelope-dark); border-left: 130px solid var(--envelope-color); bottom: 0; z-index: 9; border-radius: 0 0 15px 15px; }
        .paper { position: absolute; width: 230px; height: 140px; background: white; left: 15px; top: 10px; opacity: 0; z-index: 2; transition: all 0.8s ease-in-out; padding: 15px; border-radius: 10px; overflow: hidden; }
        
        .envelope-container.open .lid { transform: rotateX(180deg); z-index: 1; }
        .envelope-container.open .paper { opacity: 1; transform: translateY(-220px); height: 380px; z-index: 100; box-shadow: 0 10px 30px rgba(0,0,0,0.1); }
        
        .paper-content { font-family: 'Georgia', serif; font-size: 12px; color: #333; line-height: 1.5; overflow-y: auto; height: 100%; text-align: left; }
        .heart-seal { position: absolute; top: 60px; left: 50%; transform: translateX(-50%); font-size: 35px; z-index: 11; transition: 0.3s; }
        .open .heart-seal { opacity: 0; transform: translateX(-50%) scale(0); }

        .emoji-rain { position: fixed; top: -50px; z-index: 1000; animation: fall linear forwards; }
        @keyframes fall { to { transform: translateY(110vh) rotate(360deg); } }
    </style>
</head>
<body>

    <div id="decorations"></div>

    <div id="step1" class="screen active">
        <h1>Will you go on a date with me? ✨</h1>
        <div class="btn-container">
            <button id="yesBtn" onclick="goToStep(2)">YES!</button>
            <button id="noBtn" onmouseover="handleNo()" onclick="handleNo()">NO 🥺</button>
        </div>
    </div>

    <div id="step2" class="screen">
        <h1>YAY! ❤️</h1>
        <div class="bouquet-box">
            <div class="flower-emoji">💐</div>
            <div class="wrap-inner"></div><div class="wrap-outer"></div>
            <div class="emoji-ribbon"></div>
        </div>
        <p style="color: var(--primary-color); font-weight: bold;">For my beautiful lovie!</p>
        <button onclick="goToStep(3)" style="background: var(--primary-color); color: white; margin-top: 10px;">Read my letter 💌</button>
    </div>

    <div id="step3" class="screen">
        <h1>For My Lovie 💖</h1>
        <div class="envelope-container" onclick="this.classList.toggle('open')">
            <div class="heart-seal">💙</div>
            <div class="lid"></div>
            <div class="envelope-back"></div>
            <div class="envelope-front"></div>
            <div class="paper">
                <div class="paper-content">
                    <h3 style="text-align:center; color: var(--primary-color);">Hi Lovie! 👋</h3>
                    <p>
                        Hello, my beautiful lovie. Thank you for making my life colorful, just like your mood swings HEHEHE. You know I love you, and I’ll never get tired of saying it.<br><br>
                        LDR? Nah, it’s nothing when you’re the one I’m fighting for. It’s always worth it, lovie, because it’s you.<br><br>
                        I’m so sorry when I forget our monthsary or can’t give you something. Please let me make it up to you when we finally meet. I promise I will.<br><br>
                        I miss you so much, and I will always love you, my lovie.<br><br>
                        <strong>-your lovie, rainier</strong>
                    </p>
                </div>
            </div>
        </div>
        <p style="margin-top: 40px; font-size: 13px; color: #ff4d6d; font-weight: bold;">(Tap to open)</p>
    </div>

    <script>
        // Background Sparkles
        for(let i=0; i<25; i++) {
            const s = document.createElement('div');
            s.className = 'sparkle';
            s.style.left = Math.random() * 100 + 'vw';
            s.style.top = Math.random() * 100 + 'vh';
            s.style.width = s.style.height = Math.random() * 3 + 2 + 'px';
            s.style.setProperty('--duration', Math.random() * 3 + 2 + 's');
            document.getElementById('decorations').appendChild(s);
        }

        let yesScale = 1;
        let noScale = 1;

        function handleNo() {
            const noBtn = document.getElementById('noBtn');
            const yesBtn = document.getElementById('yesBtn');
            const x = Math.floor(Math.random() * 140 - 70);
            const y = Math.floor(Math.random() * 140 - 70);
            
            noScale = Math.max(0.2, noScale - 0.15); 
            yesScale += 0.2; 
            
            noBtn.style.transform = `translate(${x}px, ${y}px) scale(${noScale})`;
            yesBtn.style.transform = `scale(${yesScale})`;
        }

        function goToStep(s) {
            document.querySelectorAll('.screen').forEach(scr => scr.classList.remove('active'));
            document.getElementById('step' + s).classList.add('active');
            if(s === 2) startEmojiRain();
        }

        function startEmojiRain() {
            const emojis = ['🌸', '✨', '💖', '🌹', '💙'];
            for(let i=0; i<25; i++) {
                setTimeout(() => {
                    const e = document.createElement('div');
                    e.className = 'emoji-rain';
                    e.innerHTML = emojis[Math.floor(Math.random() * emojis.length)];
                    e.style.left = Math.random() * 100 + 'vw';
                    e.style.fontSize = '25px';
                    e.style.animationDuration = (Math.random() * 2 + 3) + 's';
                    document.body.appendChild(e);
                    setTimeout(() => e.remove(), 4000);
                }, i * 150);
            }
        }
    </script>
</body>
</html>
