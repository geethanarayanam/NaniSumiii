<html lang="te">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Anniversary Surprise</title>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Poppins:wght@300;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --heart-red: #ff0000;
            --bg-dark: #000000;
        }
        body, html { margin: 0; padding: 0; height: 100%; font-family: 'Poppins', sans-serif; overflow: hidden; background: var(--bg-dark); color: white; }
        
        /* PAGE SYSTEM */
        .page { display: none; height: 100vh; width: 100vw; flex-direction: column; align-items: center; justify-content: center; position: absolute; text-align: center; }
        .active { display: flex; animation: fadeIn 0.8s ease-in-out forwards; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* --- PAGE 1: PERFECT BIG REVOLVING HEART --- */
        #page1 { cursor: pointer; }

        /* Small Hearts Falling from Top */
        .small-heart {
            position: absolute; color: var(--heart-red);
            top: -50px; user-select: none; pointer-events: none;
            animation: fall linear forwards;
            opacity: 0.8; font-size: 20px;
        }
        @keyframes fall {
            to { transform: translateY(110vh) rotate(360deg); }
        }

        /* The BIG PERFECT HEART */
        .heart-container {
            perspective: 1000px; /* Gives it a 3D depth feel */
        }
        .big-perfect-heart {
            font-size: 200px; /* Massive size */
            color: var(--heart-red);
            display: inline-block;
            filter: drop-shadow(0 0 30px rgba(255, 0, 0, 0.8));
            animation: revolve3D 4s linear infinite;
            user-select: none;
        }
        /* Perfect Horizontal Rotation */
        @keyframes revolve3D {
            0% { transform: rotateY(0deg); }
            100% { transform: rotateY(360deg); }
        }

        .names {
            font-family: 'Dancing Script', cursive; font-size: 45px;
            margin-top: 40px; color: white;
            text-shadow: 0 0 15px var(--heart-red);
        }

        /* --- PAGE 2: GREETING --- */
        #page2 { background: #fff5f5; color: #333; }
        .card { background: white; padding: 40px; border-radius: 25px; box-shadow: 0 15px 40px rgba(0,0,0,0.15); border: 3px solid var(--heart-red); max-width: 80%; }
        
        /* --- PAGE 3: GIFT --- */
        #page3 { background: #111; }
        .gift-box { font-size: 150px; cursor: pointer; animation: pulse 1.5s infinite; }
        @keyframes pulse { 0% { transform: scale(1); } 50% { transform: scale(1.1); } 100% { transform: scale(1); } }

        /* --- PAGE 4: TEMPLE --- */
        #page4 { background: linear-gradient(135deg, #FFD700 0%, #FF8C00 100%); color: #4e342e; }
        .temple { font-size: 140px; }
        .bell { font-size: 100px; cursor: pointer; transition: 0.2s; }
        .bell:active { transform: scale(1.2); }
        .wish-box {
            background: rgba(255, 255, 255, 0.9); padding: 25px; border-radius: 15px;
            color: #900; font-weight: bold; font-size: 24px; margin-top: 30px;
            display: none; border: 3px solid #b00;
        }

        .btn { background: var(--heart-red); color: white; border: none; padding: 15px 45px; border-radius: 50px; font-size: 20px; cursor: pointer; margin-top: 30px; font-weight: bold; }
    </style>
</head>
<body onload="initHearts()">

    <div id="page1" class="page active" onclick="nextPage(2)">
        <div class="heart-container">
            <div class="big-perfect-heart">❤️</div>
        </div>
        <div class="names">Nani & Nithya</div>
        <p style="opacity: 0.6; font-size: 14px; letter-spacing: 5px; margin-top: 20px;">TAP TO ENTER</p>
    </div>

    <div id="page2" class="page">
        <div class="card">
            <h1 style="color: var(--heart-red); font-family: 'Dancing Script'; font-size: 50px; margin: 0;">Happy Anniversary!</h1>
            <p style="font-size: 24px;"><b>Nani & Nithya</b></p>
            <p>May your love story continue to grow and inspire everyone around you.</p>
            <button class="btn" onclick="nextPage(3)">Unwrap Gift 🎁</button>
        </div>
    </div>

    <div id="page3" class="page">
        <div class="gift-box" onclick="openGift()">🎁</div>
        <h2 id="gift-msg" style="color: white;">A surprise awaits!</h2>
        <button id="temple-btn" class="btn" style="display:none;" onclick="nextPage(4)">Seek Blessings 🙏🏼</button>
    </div>

    <div id="page4" class="page">
        <div class="temple">🛕</div>
        <div class="bell" id="bell" onclick="ringBell()">🔔</div>
        <p style="font-weight: bold;">Ring the bell for the couple!</p>
        <div id="teluguWish" class="wish-box">
            నాని & నిత్య వివాహ వార్షికోత్సవ శుభాకాంక్షలు!<br>
            మీరు కలకాలం సుఖసంతోషాలతో వర్ధిల్లాలని కోరుకుంటున్నాను. 🙏
        </div>
    </div>

    <script>
        function initHearts() {
            // Generates small hearts falling from top
            setInterval(() => {
                const h = document.createElement('div');
                h.className = 'small-heart';
                h.innerHTML = '❤️';
                h.style.left = Math.random() * 100 + 'vw';
                h.style.animationDuration = Math.random() * 3 + 2 + 's';
                document.getElementById('page1').appendChild(h);
                setTimeout(() => h.remove(), 5000);
            }, 400);
        }

        function nextPage(n) {
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            document.getElementById('page' + n).classList.add('active');
        }

        function openGift() {
            document.querySelector('.gift-box').innerHTML = '💖';
            document.getElementById('gift-msg').innerText = "Lots of love to you!";
            document.getElementById('temple-btn').style.display = 'block';
            // Sparkle burst
            for(let i=0; i<40; i++) {
                let s = document.createElement('div');
                s.style.position = 'fixed';
                s.style.left = '50%'; s.style.top = '50%';
                s.style.width = '6px'; s.style.height = '6px';
                s.style.background = 'gold';
                s.style.borderRadius = '50%';
                document.body.appendChild(s);
                s.animate([
                    { transform: 'translate(0,0)', opacity: 1 },
                    { transform: `translate(${(Math.random()-0.5)*800}px, ${(Math.random()-0.5)*800}px)`, opacity: 0 }
                ], { duration: 1500, fill: 'forwards' });
                setTimeout(() => s.remove(), 1500);
            }
        }

        function ringBell() {
            const bell = document.getElementById('bell');
            bell.style.transform = "rotate(20deg)";
            setTimeout(() => bell.style.transform = "rotate(-20deg)", 150);
            setTimeout(() => bell.style.transform = "rotate(0deg)", 300);
            document.getElementById('teluguWish').style.display = 'block';
            document.getElementById('teluguWish').animate([{opacity: 0}, {opacity: 1}], {duration: 1000, fill: 'forwards'});
        }
    </script>
</body>
</html>
