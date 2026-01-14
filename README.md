<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy 15th Birthday Navya!</title>
    <style>
        /* --- CSS STYLES --- */
        body {
            margin: 0;
            padding: 0;
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #fdfbfb 0%, #ebedee 100%);
            overflow: hidden; /* Prevent scrolling */
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            text-align: center;
        }

        /* Container for all slides */
        .container {
            width: 100%;
            height: 100%;
            position: relative;
        }

        /* Slide Classes */
        .slide {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background: linear-gradient(to bottom, #fff0f5, #e6e6fa); /* Soft pink to lavender */
            opacity: 0;
            visibility: hidden;
            transition: opacity 1s ease-in-out;
            z-index: 1;
        }

        .slide.active {
            opacity: 1;
            visibility: visible;
            z-index: 2;
        }

        /* Typography */
        h1 {
            color: #d4af37; /* Gold */
            font-size: 3rem;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
            margin: 10px;
        }
        
        h2 {
            color: #b76e79; /* Rose Gold */
            font-size: 2rem;
        }

        p {
            color: #555;
            font-size: 1.2rem;
        }

        /* Slide 1: Hero */
        .big-number {
            font-size: 8rem;
            color: #ff69b4;
            font-weight: bold;
            animation: float 3s ease-in-out infinite;
        }

        /* Slide 2: Gift Box */
        .gift-box {
            font-size: 8rem;
            cursor: pointer;
            animation: wiggle 2s infinite;
        }

        /* Slide 3: Cake */
        .cake {
            font-size: 6rem;
            cursor: pointer;
        }
        .candles {
            font-size: 1rem;
            color: orange;
            animation: flicker 0.5s infinite;
        }

        /* Slide 4: Balloon */
        .balloon-container {
            position: relative;
        }
        .balloon {
            font-size: 8rem;
            cursor: pointer;
            color: #ff4d6d;
            animation: float 4s ease-in-out infinite;
            display: block;
        }
        .hidden-message {
            display: none;
            font-size: 3rem;
            color: #d90429;
            font-weight: bold;
            animation: popIn 0.5s ease-out;
        }

        /* Slide 5: Final Message */
        .card {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
            max-width: 80%;
            border: 2px solid #b76e79;
        }

        /* Button */
        .btn {
            margin-top: 20px;
            padding: 10px 20px;
            background-color: #b76e79;
            color: white;
            border: none;
            border-radius: 25px;
            font-size: 1.2rem;
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(183, 110, 121, 0.4);
        }

        /* Animations */
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
            100% { transform: translateY(0px); }
        }

        @keyframes wiggle {
            0%, 100% { transform: rotate(0deg); }
            25% { transform: rotate(-5deg); }
            75% { transform: rotate(5deg); }
        }

        @keyframes flicker {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }

        @keyframes popIn {
            0% { transform: scale(0); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }

        /* Confetti Canvas */
        #confetti {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 100;
        }
    </style>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
</head>
<body>

    <div class="container">
        
        <div class="slide active" id="slide1">
            <h1>It's Finally Here...</h1>
            <div class="big-number">15</div>
            <h2>Happy Birthday Navya!</h2>
            <p>14th January</p>
            <button class="btn" onclick="nextSlide(2)">Start the Celebration</button>
        </div>

        <div class="slide" id="slide2">
            <h1>I have a surprise for you...</h1>
            <div class="gift-box" onclick="openGift()">🎁</div>
            <p>(Tap the box to open)</p>
        </div>

        <div class="slide" id="slide3">
            <h1>Make a Wish!</h1>
            <div class="cake">🎂</div>
            <p>May all your dreams come true.</p>
            <button class="btn" onclick="nextSlide(4)">Cut the Cake & Continue</button>
        </div>

        <div class="slide" id="slide4">
            <h1>One last balloon...</h1>
            <div class="balloon-container">
                <div class="balloon" id="popBalloon" onclick="popBalloon()">🎈</div>
                <div class="hidden-message" id="loveMessage">I Love You ❤️</div>
            </div>
            <p id="balloonText">(Tap the balloon to pop it!)</p>
            <button class="btn" id="finalBtn" style="display:none;" onclick="nextSlide(5)">See who sent this</button>
        </div>

        <div class="slide" id="slide5">
            <div class="card">
                <h2>Happy 15th Birthday, Navya</h2>
                <p>Wishing you a year as beautiful and amazing as you are. Enjoy your special day!</p>
                <br>
                <p>With love,</p>
                <h3>Amaresh Rai</h3>
            </div>
        </div>

    </div>

    <script>
        /* --- JAVASCRIPT LOGIC --- */
        
        function nextSlide(slideNumber) {
            // Hide all slides
            document.querySelectorAll('.slide').forEach(slide => {
                slide.classList.remove('active');
            });
            // Show requested slide
            document.getElementById('slide' + slideNumber).classList.add('active');
        }

        function openGift() {
            // Trigger Confetti
            confetti({
                particleCount: 100,
                spread: 70,
                origin: { y: 0.6 }
            });
            // Wait 1 second then go to cake
            setTimeout(() => {
                nextSlide(3);
            }, 1000);
        }

        function popBalloon() {
            // "Pop" the balloon
            document.getElementById('popBalloon').style.display = 'none';
            document.getElementById('balloonText').style.display = 'none';
            
            // Show Message
            document.getElementById('loveMessage').style.display = 'block';
            document.getElementById('finalBtn').style.display = 'inline-block';

            // Trigger Confetti
            var duration = 2 * 1000;
            var animationEnd = Date.now() + duration;
            var defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 0 };

            var interval = setInterval(function() {
                var timeLeft = animationEnd - Date.now();

                if (timeLeft <= 0) {
                    return clearInterval(interval);
                }

                var particleCount = 50 * (timeLeft / duration);
                confetti(Object.assign({}, defaults, { particleCount, origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 } }));
                confetti(Object.assign({}, defaults, { particleCount, origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 } }));
            }, 250);
        }

        function randomInRange(min, max) {
            return Math.random() * (max - min) + min;
        }
    </script>
</body>
</html>
