# ucapan_kasih_sayang
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ucapan Kasih Sayang</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background-color: cyan;
            color: white;
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            text-align: center;
            position: relative;
        }
        canvas {
            position: absolute;
            top: 0;
            left: 0;
            z-index: 0;
        }
        #message {
            position: relative;
            z-index: 1;
            font-size: 24px;
            text-align: center;
        }
    </style>
</head>
<body>
    <div id="message"></div>
    <canvas id="canvas"></canvas>
    
    <script>
        function ucapanKasihSayang(nama) {
            return `Hai ${nama},<br>
            Aku ingin kamu tahu betapa berartinya kamu bagiku.<br>
            Setiap hari bersamamu adalah anugerah yang luar biasa.<br>
            Terima kasih telah menjadi sumber kebahagiaan dalam hidupku.<br>
            Aku mencintaimu sekarang dan selamanya!`;
        }

        const namaPacar = prompt("Masukkan nama pacarmu:", "Aisyah");
        const messageDiv = document.getElementById('message');
        messageDiv.innerHTML = ucapanKasihSayang(namaPacar);

        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        let stars = [];
        const starCount = 100;

        for (let i = 0; i < starCount; i++) {
            stars.push({
                x: Math.random() * canvas.width,
                y: Math.random() * canvas.height,
                radius: Math.random() * 3 + 1,
                speedX: Math.random() * 0.5 - 0.25,
                speedY: Math.random() * 0.5 - 0.25
            });
        }

        // Doll properties
        let doll = {
            x: Math.random() * canvas.width,
            y: Math.random() * canvas.height,
            size: 30,
            speedX: Math.random() * 3 + 1,
            speedY: Math.random() * 3 + 1
        };

        function drawStars() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            stars.forEach(star => {
                ctx.beginPath();
                ctx.arc(star.x, star.y, star.radius, 0, Math.PI * 2);
                ctx.fillStyle = 'white';
                ctx.fill();
            });
        }

        function updateStars() {
            stars.forEach(star => {
                star.x += star.speedX;
                star.y += star.speedY;

                // Bounce off walls
                if (star.x < 0 || star.x > canvas.width) {
                    star.speedX *= -1;
                }
                if (star.y < 0 || star.y > canvas.height) {
                    star.speedY *= -1;
                }
            });
        }

        function drawDoll() {
            // Draw head
            ctx.fillStyle = 'pink';
            ctx.beginPath();
            ctx.arc(doll.x, doll.y - 15, doll.size, 0, Math.PI * 2);
            ctx.fill();
            // Draw body
            ctx.fillStyle = 'purple';
            ctx.fillRect(doll.x - doll.size / 4, doll.y - 15, doll.size / 2, doll.size); 
            // Draw arms
            ctx.fillStyle = 'pink';
            ctx.fillRect(doll.x - doll.size, doll.y - 15, doll.size / 4, doll.size / 2); 
            ctx.fillRect(doll.x + doll.size / 4, doll.y - 15, doll.size / 4, doll.size / 2); 
        }

        function updateDoll() {
            doll.x += doll.speedX;
            doll.y += doll.speedY;

            // Bounce off walls
            if (doll.x < doll.size || doll.x > canvas.width - doll.size) {
                doll.speedX *= -1;
            }
            if (doll.y < doll.size || doll.y > canvas.height - doll.size) {
                doll.speedY *= -1;
            }
        }

        function animate() {
            updateStars();
            drawStars();
            updateDoll();
            drawDoll();
            requestAnimationFrame(animate);
        }

        animate();
    </script>
</body>
</html>
