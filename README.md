<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday! 🎉</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-pink: #ff4d94;
            --soft-pink: #ffb3d1;
            --deep-pink: #ff0066;
        }

        body {
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: radial-gradient(circle at center, #4d0026 0%, #1a000a 100%);
            font-family: 'Poppins', sans-serif;
            overflow: hidden;
            transition: background 1.5s ease;
        }

        #cursor-glow {
            position: fixed;
            width: 300px;
            height: 300px;
            background: radial-gradient(circle, rgba(255, 77, 148, 0.2) 0%, transparent 70%);
            border-radius: 50%;
            pointer-events: none;
            transform: translate(-50%, -50%);
            z-index: 1;
        }

        .heart-float {
            position: absolute;
            color: var(--primary-pink);
            font-size: 20px;
            pointer-events: none;
            z-index: 0;
            animation: floatUp 6s linear forwards;
        }

        @keyframes floatUp {
            0% { transform: translateY(100vh) rotate(0deg); opacity: 1; }
            100% { transform: translateY(-10vh) rotate(360deg); opacity: 0; }
        }

        .card {
            position: relative;
            z-index: 10;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(15px);
            -webkit-backdrop-filter: blur(15px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            padding: 40px;
            border-radius: 30px;
            box-shadow: 0 8px 32px 0 rgba(255, 77, 148, 0.37);
            text-align: center;
            max-width: 450px;
            width: 85%;
            color: white;
            transition: opacity 0.5s ease;
        }

        .hidden { display: none !important; }

        h1 { color: var(--primary-pink); font-size: 2.2rem; margin-bottom: 15px; }
        p { font-weight: 300; line-height: 1.7; margin-bottom: 20px; }

        .btn {
            background: linear-gradient(45deg, var(--primary-pink), var(--deep-pink));
            color: white;
            border: none;
            padding: 15px 35px;
            border-radius: 50px;
            font-weight: 600;
            cursor: pointer;
            transition: 0.2s;
            box-shadow: 0 5px 15px rgba(255, 0, 102, 0.4);
            margin: 10px;
        }

        .btn-exit {
            background: #444;
            margin-top: 30px;
            font-size: 0.8rem;
            padding: 10px 20px;
            opacity: 0.8;
        }

        input {
            background: rgba(255, 255, 255, 0.1);
            border: 2px solid var(--soft-pink);
            padding: 10px;
            border-radius: 10px;
            color: white;
            width: 70px;
            text-align: center;
            font-size: 1.1rem;
            margin: 10px 0;
            outline: none;
        }

        #next-icon {
            font-size: 40px;
            cursor: pointer;
            color: var(--primary-pink);
            margin-top: 20px;
            display: inline-block;
            animation: bounceRight 1s infinite alternate;
        }

        @keyframes bounceRight {
            from { transform: translateX(0); }
            to { transform: translateX(10px); }
        }

        .choice-container {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-wrap: wrap;
            min-height: 150px;
        }

        #no-btn { background: #555; box-shadow: none; }

        .thank-you-heart {
            font-size: 80px;
            animation: pulse 1.5s infinite;
            display: block;
            margin-bottom: 20px;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); }
            100% { transform: scale(1); }
        }

        #exit-overlay {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: black;
            z-index: 1000;
            display: none;
            justify-content: center;
            align-items: center;
            color: var(--primary-pink);
            font-size: 1.5rem;
            text-align: center;
            opacity: 0;
            transition: opacity 1.5s ease;
        }
    </style>
</head>
<body>

    <div id="cursor-glow"></div>
    <div id="exit-overlay">See you later! 👋<br>Have a beautiful day! 💖</div>

    <div class="card" id="page1">
        <div style="font-size: 60px;">🎁</div>
        <h1>Hey Friend!</h1>
        <p>I have a little something special waiting for you. Are you ready to see it?</p>
        <button class="btn" onclick="showPage('page1', 'page2')">Open My Surprise ✨</button>
    </div>

    <div class="card hidden" id="page2">
        <div style="font-size: 50px;">💖</div>
        <h1>Happy Birthday!</h1>
        <p>
            On this incredibly special day, I wanted to take a moment to tell you how amazing you are. 
            May your year be filled with endless laughter, beautiful moments, and all the success you've been working so hard for. 
            Keep shining your bright light on the world—you make everything better just by being you! 🌟
        </p>
        
        <div style="border-top: 1px solid rgba(255,255,255,0.2); padding-top: 20px;">
            <p><strong>Wait! Time flies so fast...</strong></p>
            <label for="age">How many years old are you today? 🎂</label><br>
            <input type="number" id="age" placeholder="??"><br>
            <button class="btn" style="padding: 10px 25px;" onclick="submitAge()">Submit</button>
            <div id="next-container" class="hidden">
                <p id="response-msg"></p>
                <div id="next-icon" onclick="showPage('page2', 'page3')">⮕</div>
            </div>
        </div>
    </div>

    <div class="card hidden" id="page3">
        <div style="font-size: 60px;">🥳</div>
        <h1>Party Time!</h1>
        <p>So... since it's your birthday, are you going to give me a party? 🍕🎂</p>
        <div class="choice-container">
            <button class="btn" id="yes-btn" onclick="showPage('page3', 'page4')">YES! 😍</button>
            <button class="btn" id="no-btn" onclick="shrinkNo()">No 😢</button>
        </div>
    </div>

    <div class="card hidden" id="page4">
        <span class="thank-you-heart">💖</span>
        <h1>Thank You!</h1>
        <p>
            Thank you so much for being such a wonderful part of my life. 
            I'm so glad we could celebrate your day like this! 
            Hope you have the most magical birthday ever. ✨🌸
        </p>
        <button class="btn btn-exit" onclick="exitPage()">Exit Experience 🚪</button>
    </div>

    <script>
        const glow = document.getElementById('cursor-glow');
        document.addEventListener('mousemove', (e) => {
            glow.style.left = e.clientX + 'px';
            glow.style.top = e.clientY + 'px';
        });

        setInterval(() => {
            const heart = document.createElement('div');
            heart.className = 'heart-float';
            heart.innerHTML = ['💖', '💗', '🌸', '✨', '🎈'][Math.floor(Math.random() * 5)];
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = (Math.random() * 3 + 4) + 's';
            document.body.appendChild(heart);
            setTimeout(() => heart.remove(), 6000);
        }, 400);

        function showPage(curr, next) {
            spawnParticles();
            document.getElementById(curr).classList.add('hidden');
            document.getElementById(next).classList.remove('hidden');
        }

        function submitAge() {
            const age = document.getElementById('age').value;
            if(age) {
                document.getElementById('response-msg').innerHTML = `Wow, ${age}! You're growing up so fast! 🎈`;
                document.getElementById('next-container').classList.remove('hidden');
                spawnParticles();
            }
        }

        let yesFontSize = 16;
        let noFontSize = 16;
        let paddingAmt = 15;

        function shrinkNo() {
            const noBtn = document.getElementById('no-btn');
            const yesBtn = document.getElementById('yes-btn');
            
            noFontSize -= 4;
            yesFontSize += 8;
            paddingAmt += 5;

            if (noFontSize <= 0) {
                noBtn.style.display = 'none';
            } else {
                noBtn.style.fontSize = noFontSize + 'px';
                noBtn.style.padding = '5px 10px';
            }

            yesBtn.style.fontSize = yesFontSize + 'px';
            yesBtn.style.padding = `${paddingAmt}px ${paddingAmt * 2}px`;
        }

        function exitPage() {
            const overlay = document.getElementById('exit-overlay');
            overlay.style.display = 'flex';
            setTimeout(() => {
                overlay.style.opacity = '1';
            }, 10);
            // Optional: tries to close window, but usually blocked by browsers
            setTimeout(() => {
                window.close();
            }, 3000);
        }

        function spawnParticles() {
            for(let i=0; i<40; i++) {
                const p = document.createElement('div');
                p.style.position = 'fixed';
                p.style.left = '50%'; p.style.top = '50%';
                p.style.width = '8px'; p.style.height = '8px';
                p.style.backgroundColor = ['#ff4d94', '#ff0066', '#ffffff'][Math.floor(Math.random()*3)];
                p.style.borderRadius = '50%';
                p.style.pointerEvents = 'none';
                document.body.appendChild(p);
                const destX = (Math.random() - 0.5) * 1200;
                const destY = (Math.random() - 0.5) * 1200;
                p.animate([
                    { transform: 'translate(0, 0) scale(1)', opacity: 1 },
                    { transform: `translate(${destX}px, ${destY}px) scale(0)`, opacity: 0 }
                ], { duration: 1500, easing: 'ease-out' }).onfinish = () => p.remove();
            }
        }
    </script>
</body>
</html>
