<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy New Year 2026 | My Love</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --love-red: #ff4d6d;
            --glass: rgba(255, 255, 255, 0.12);
            --gold: #ffb703;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            background: #0a0908;
            color: white;
            font-family: 'Poppins', sans-serif;
            height: 100vh;
            overflow: hidden;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            touch-action: pan-y; /* Allows scrolling but prevents accidental zooming */
        }

        canvas { position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 1; }

        .carousel-wrapper {
            position: relative;
            z-index: 10;
            width: 90%;
            max-width: 450px;
            height: 80vh;
            display: flex;
            flex-direction: column;
        }

        .top-nav { display: flex; justify-content: flex-end; gap: 10px; margin-bottom: 10px; }

        .icon-btn {
            background: var(--glass);
            border: 1px solid rgba(255,255,255,0.2);
            color: white;
            width: 45px; height: 45px;
            border-radius: 50%;
            cursor: pointer;
            backdrop-filter: blur(10px);
        }

        .slides-container { flex: 1; position: relative; }

        .slide {
            position: absolute;
            inset: 0;
            background: var(--glass);
            backdrop-filter: blur(25px);
            border: 1px solid rgba(255,255,255,0.1);
            border-radius: 25px;
            padding: 25px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-align: center;
            opacity: 0;
            transform: translateX(50px);
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
            pointer-events: none;
        }

        .slide.active { opacity: 1; transform: translateX(0); pointer-events: auto; }

        h1 { font-family: 'Dancing Script', cursive; font-size: 2rem; color: var(--love-red); margin-bottom: 10px; }
        
        /* Memory Grid Fix for Mobile */
        .memory-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-top: 15px;
            width: 100%;
        }

        .memory-item {
            width: 100%; height: 110px;
            border-radius: 12px;
            object-fit: cover;
            border: 2px solid rgba(255,255,255,0.1);
            background: #222;
        }

        .nav-arrows {
            position: absolute;
            width: 110%;
            left: -5%;
            top: 50%;
            display: flex;
            justify-content: space-between;
            pointer-events: none;
            z-index: 100;
        }

        .arrow {
            pointer-events: auto;
            background: white;
            color: var(--love-red);
            width: 40px; height: 40px;
            border-radius: 50%;
            border: none;
            cursor: pointer;
        }

        .sig { font-family: 'Dancing Script', cursive; font-size: 1.8rem; color: var(--gold); margin-top: 15px; }

        footer { margin-top: 15px; font-size: 0.7rem; letter-spacing: 2px; opacity: 0.6; }
    </style>
</head>
<body>

    <canvas id="fireworks"></canvas>
    <canvas id="hearts"></canvas>

    <div class="carousel-wrapper" id="swipeArea">
        <div class="top-nav">
            <button class="icon-btn" onclick="toggleAuto()"><i id="autoIcon" class="fas fa-play"></i></button>
            <button class="icon-btn" onclick="toggleMusic()"><i id="musicIcon" class="fas fa-music"></i></button>
        </div>

        <div class="slides-container">
            <div class="slide active">
                <h1>Happy New Year 2026, My Love ❤️</h1>
                <p>Every second with you is a gift. Let's make 2026 our best year yet.</p>
                <p style="margin-top: 10px; font-style: italic; font-size: 0.8rem;">"You're my forever plus a day."</p>
            </div>

            <div class="slide">
                <h3>Our Memories</h3>
                <div class="memory-grid">
                    <img src="photo1.jpg" class="memory-item" onerror="this.src='https://via.placeholder.com/150?text=Upload+Photo1'">
                    <video class="memory-item" loop muted autoplay playsinline webkit-playsinline src="video1.mp4"></video>
                    <img src="photo2.jpg" class="memory-item" onerror="this.src='https://via.placeholder.com/150?text=Upload+Photo2'">
                    <img src="photo3.jpg" class="memory-item" onerror="this.src='https://via.placeholder.com/150?text=Upload+Photo3'">
                </div>
            </div>

            <div class="slide">
                <h3>My Promise</h3>
                <p>To my best friend, my soulmate, and my home: I love you more than words can express.</p>
                <div class="sig">Yours, Bibek</div>
            </div>

            <div class="nav-arrows">
                <button class="arrow" onclick="changeSlide(-1)"><i class="fas fa-chevron-left"></i></button>
                <button class="arrow" onclick="changeSlide(1)"><i class="fas fa-chevron-right"></i></button>
            </div>
        </div>
    </div>

    <footer>FOREVER & ALWAYS ✨</footer>

    <audio id="bgMusic" loop>
        <source src="music.mp3" type="audio/mpeg">
    </audio>

    <script>
        let currentSlide = 0;
        const slides = document.querySelectorAll('.slide');
        let autoInterval;

        function changeSlide(dir) {
            slides[currentSlide].classList.remove('active');
            currentSlide = (currentSlide + dir + slides.length) % slides.length;
            slides[currentSlide].classList.add('active');
        }

        // SWIPE SUPPORT FOR PHONE
        let touchstartX = 0;
        let touchendX = 0;
        const swipeArea = document.getElementById('swipeArea');

        swipeArea.addEventListener('touchstart', e => { touchstartX = e.changedTouches[0].screenX; });
        swipeArea.addEventListener('touchend', e => {
            touchendX = e.changedTouches[0].screenX;
            if (touchendX < touchstartX - 50) changeSlide(1); // Swipe Left
            if (touchendX > touchstartX + 50) changeSlide(-1); // Swipe Right
        });

        function toggleAuto() {
            const icon = document.getElementById('autoIcon');
            if (autoInterval) {
                clearInterval(autoInterval);
                autoInterval = null;
                icon.classList.replace('fa-pause', 'fa-play');
            } else {
                autoInterval = setInterval(() => changeSlide(1), 4000);
                icon.classList.replace('fa-play', 'fa-pause');
            }
        }

        function toggleMusic() {
            const music = document.getElementById('bgMusic');
            const icon = document.getElementById('musicIcon');
            if (music.paused) { music.play(); icon.style.color = "#ff4d6d"; }
            else { music.pause(); icon.style.color = "white"; }
        }

        // --- ANIMATIONS (FIREWORKS/HEARTS) ---
        const hCanvas = document.getElementById('hearts');
        const hctx = hCanvas.getContext('2d');
        const fCanvas = document.getElementById('fireworks');
        const fctx = fCanvas.getContext('2d');

        function resize() {
            hCanvas.width = fCanvas.width = window.innerWidth;
            hCanvas.height = fCanvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resize);
        resize();

        let hearts = [];
        class Heart {
            constructor() {
                this.x = Math.random() * hCanvas.width;
                this.y = hCanvas.height + 20;
                this.size = Math.random() * 10 + 5;
                this.speed = Math.random() * 2 + 1;
                this.opacity = 1;
            }
            draw() {
                hctx.globalAlpha = this.opacity;
                hctx.fillStyle = '#ff4d6d';
                hctx.beginPath();
                hctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                hctx.fill();
            }
            update() { this.y -= this.speed; this.opacity -= 0.005; }
        }

        let particles = [];
        function createFw(x, y) {
            for(let i=0; i<20; i++) {
                particles.push({
                    x, y,
                    dx: (Math.random()-0.5)*6,
                    dy: (Math.random()-0.5)*6,
                    c: `hsl(${Math.random()*360}, 100%, 50%)`,
                    l: 80
                });
            }
        }

        function animate() {
            hctx.clearRect(0,0,hCanvas.width, hCanvas.height);
            fctx.fillStyle = 'rgba(10, 9, 8, 0.2)';
            fctx.fillRect(0,0,fCanvas.width, fCanvas.height);

            if(Math.random() < 0.05) hearts.push(new Heart());
            hearts.forEach((h, i) => {
                h.update(); h.draw();
                if(h.opacity <= 0) hearts.splice(i, 1);
            });

            if(Math.random() < 0.03) createFw(Math.random()*fCanvas.width, Math.random()*fCanvas.height*0.5);
            particles.forEach((p, i) => {
                p.x += p.dx; p.y += p.dy; p.l--;
                fctx.fillStyle = p.c;
                fctx.fillRect(p.x, p.y, 2, 2);
                if(p.l <= 0) particles.splice(i, 1);
            });
            requestAnimationFrame(animate);
        }
        animate();
    </script>
</body>
</html>
