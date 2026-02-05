# MyLovie
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For My Lovie 💌</title>
    <style>
        :root {
            --primary-color: #ff4d6d;
            --glass-bg: rgba(255, 255, 255, 0.45);
            --envelope-color: #ffb1c1;
            --envelope-dark: #ff8fa3;
            --wrap-outer: #ffb1c1;
            --wrap-inner: #ffd1dc;
            --ribbon-color: #e63946;
        }

        body, html {
            margin: 0; padding: 0;
            width: 100%; height: 100%;
            display: flex; justify-content: center; align-items: center;
            background: linear-gradient(-45deg, #ffdee9, #fff0f6, #e0c3fc, #b5fffc);
            background-size: 400% 400%;
            animation: gradient 15s ease infinite;
            font-family: 'Comic Sans MS', 'Arial', sans-serif;
            overflow: hidden; position: relative;
            user-select: none;
        }

        @keyframes gradient { 0% { background-position: 0% 50%; } 50% { background-position: 100% 50%; } 100% { background-position: 0% 50%; } }

        .sparkle { position: absolute; background: white; border-radius: 50%; opacity: 0.8; z-index: 2; animation: twinkle var(--duration) ease-in-out infinite; }
        @keyframes twinkle { 0%, 100% { transform: scale(0); opacity: 0; } 50% { transform: scale(1); opacity: 1; } }

        /* Main Container Centering */
        .screen {
            display: none; flex-direction: column; align-items: center; justify-content: center;
            text-align: center; width: 90%; max-width: 400px; z-index: 10;
            background: var(--glass-bg); backdrop-filter: blur(15px);
            padding: 40px 20px; border-radius: 40px; border: 1px solid rgba(255, 255, 255, 0.7);
            box-shadow: 0 20px 45px rgba(0,0,0,0.08);
            position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);
        }

        .active { display: flex; animation: fadeIn 0.5s ease-out; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        h1 { color: var(--primary-color); font-size: 24px; margin-bottom: 20px; text-shadow: 1px 1px 4px white; }

        /* Step 1 Button Layout */
        .btn-container { 
            position: relative; display: flex; justify-content: center; align-items: center; 
            width: 100%; min-height: 250px; 
        }
        
        button { 
            padding: 14px 35px; font-size: 18px; cursor: pointer; border-radius: 50px; border: none; 
            font-weight: bold; box-shadow: 0 10px 20px rgba(0,0,0,0.1); 
            transition: transform 0.1s ease; 
            touch-action: manipulation;
        }

        #yesBtn { background: var(--primary-color); color: white; z-index: 100; position: relative; }
        #noBtn { background: white; color: var(--primary-color); border: 2px solid var(--primary-color); position: absolute; z-index: 50; }

        /* Bouquet Styling */
        .bouquet-box {
            position: relative; width: 220px; height: 260px;
            display: flex; justify-content: center; align-items: center;
            margin: 10px 0; animation: float 4s ease-in-out infinite;
        }
        .flower-emoji { font-size: 115px; z-index: 10; position: relative; top: -25px; filter: drop-shadow(0 5px 10px rgba(0,0,0,0.15)); }
        .wrap-inner { position: absolute; bottom: 45px; width: 100px; height: 130px; background: var(--wrap-inner); background-image: radial-gradient(white 1px, transparent 1px); background-size: 8px 8px; clip-path: polygon(10% 0%, 90% 0%, 100% 100%, 0% 100%); z-index: 8; opacity: 0.9; border-top: 2px dashed white; }
        .wrap-outer { position: absolute; bottom: 30px; width: 120px; height: 140px; background: var(--wrap-outer); clip-path: polygon(0% 15%, 100% 15%, 80% 100%, 20% 100%); z-index: 7; }
        .stem-bunch { position: absolute; bottom: 10px; display: flex; gap: 4px; z-index: 5; }
        .st-line { width: 4px; height: 35px; background: #2d6a4f; border-radius: 4px; }
        .st1 { transform: rotate(-10deg); } .st2 { height: 40px; } .st3 { transform: rotate(10deg); }
        .emoji-ribbon { position: absolute; bottom: 60px; width: 110px; height: 16px; background: var(--ribbon-color); border-radius: 20px; z-index: 15; }
        .ribbon-knot { position: absolute; width: 20px; height: 20px; background: var(--ribbon-color); border-radius: 50%; top: 50%; left: 50%; transform: translate(-50%, -50%); border: 2px solid rgba(255,255,255,0.3); }

        @keyframes float { 0%, 100% { transform: translateY(0) rotate(-1deg); } 50% { transform: translateY(-15px) rotate(1deg); } }

        /* Envelope Surprise */
        .envelope-container { position: relative; width: 280px; height: 180px; cursor: pointer; margin-top: 20px; perspective: 1000px; }
        .envelope-back { position: absolute; width: 100%; height: 100%; background: var(--envelope-color); border-radius: 0 0 15px 15px; z-index: 1; }
        .lid { position: absolute; width: 0; height: 0; border-top: 100px solid var(--envelope-dark); border-left: 140px solid transparent; border-right: 140px solid transparent; top: 0; left: 0; transform-origin: top; transition: transform 0.6s ease; z-index: 10; }
        .envelope-front { position: absolute; width: 0; height: 0; border-right: 140px solid var(--envelope-color); border-bottom: 90px solid var(--envelope-dark); border-left: 140px solid var(--envelope-color); bottom: 0; z-index: 9; border-radius: 0 0 15px 15px; }
        .paper { position: absolute; width: 250px; height: 160px; background: white; left: 15px; top: 15px; opacity: 0; z-index: 2; transition: transform 0.8s ease-in-out, height 0.8s ease-in-out, opacity 0.3s; padding: 25px; box-sizing: border-box; border-radius: 10px; overflow: hidden; }
        .envelope-container.open .lid { transform: rotateX(180deg); z-index: 1; }
        .envelope-container.open .paper { opacity: 1; transform: translateY(-240px); height: 420px; z-index: 100; box-shadow: 0 10px 30px rgba(0,0,0,0.1); }
        .paper-content { font-family: 'Georgia', serif; font-size: 13px; color: #333; line-height: 1.6; overflow-y: auto; height: 100%; text-align: left; }
        .heart-seal { position: absolute; top: 70px; left: 50%; transform: translateX(-50%); font-size: 38px; z-index: 11; transition: 0.3s; }
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
            <button id="noBtn" onmouseover="handleNoInteraction()" onclick="handleNoInteraction()">NO 🥺</button>
        </div>
    </div>

    <div id="step2" class="screen">
        <h1>YAY! See you soon, Lovie! ❤️</h1>
        <div class="bouquet-box">
            <div class="flower-emoji">💐</div>
            <div class="wrap-inner"></div>
            <div class="wrap-outer"></div>
            <div class="stem-bunch">
                <div class="st-line st1"></div><div class="st-line st2"></div><div class="st-line st3"></div>
            </div>
            <div class="emoji-ribbon"><div class="ribbon-knot"></div></div>
        </div>
        <p style="color: var(--primary-color); font-weight: bold; font-size: 16px;">A beautiful bouquet for my beautiful lovie!</p>
        <button onclick="goToStep(3)" style="background: var(--primary-color); color: white; margin-top: 10px;">Read my letter 💌</button>
    </div>

    <div id="step3" class="screen">
        <h1 style="font-size: 22px;">For My Lovie 💖</h1>
        <div class="envelope-container" id="env" onclick="this.classList.toggle('open')">
            <div class="heart-seal">💙</div>
            <div class="lid"></div>
            <div class="envelope-back"></div>
            <div class="envelope-front"></div>
            <div class="paper">
                <div class="paper-content">
                    <h3 style="text-align:center; color: var(--primary-color); margin-top:0;">Hi Lovie! 👋</h3>
                    <p>
                        Hello, my beautiful lovie. Thank you for making my life colorful, just like your mood swings HEHEHE. You know I love you, and I’ll never get tired of saying it, even if you do get bored with hearing it.<br><br>
                        LDR? Nah, it’s nothing when you’re the one I’m fighting for. It’s always worth it, lovie, because it’s you. After this long-distance phase, everything we’ve been through will be worth it, and we’ll finally be together—until you get tired of seeing my face.<br><br>
                        I’m so sorry, lovie, when I forget our monthsary and when I can’t do anything or give you something. I know we can’t always celebrate our occasions and monthsaries while we’re far from each other. But please let me make it up to you when we finally meet and spend time together—I promise I will.<br><br>
                        I miss you so much, and I will always love you, my lovie.<br><br>
                        <strong>-your lovie, rainier</strong>
                    </p>
                </div>
            </div>
        </div>
        <p style="margin-top: 50px; font-size: 14px; color: #ff4d6d; font-weight: bold;">(Tap to open the letter)</p>
    </div>

    <script>
        // Sparkle background logic
        const decor = document.getElementById('decorations');
        for(let i=0; i<30; i++) {
            const s = document.createElement('div');
            s.className = 'sparkle';
            s.style.left = Math.random() * 100 + 'vw';
            s.style.top = Math.random() * 100 + 'vh';
            s.style.width = s.style.height = Math.random() * 4 + 2 + 'px';
            s.style.setProperty('--duration', Math.random() * 3 + 2 + 's');
            decor.appendChild(s);
        }

        let yesScale = 1;
        let noScale = 1;

        function handleNoInteraction() {
            const noBtn = document.getElementById('noBtn');
            const yesBtn = document.getElementById('yesBtn');
            
            // Randomized movement for NO button
            const x = Math.floor(Math.random() * 180 - 90);
            const y = Math.floor(Math.random() * 180 - 90);
            
            noScale = Math.max(0.1, noScale - 0.1); 
            yesScale += 0.2; // 20% Growth
            
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
            for(let i=0; i<30; i++) {
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
