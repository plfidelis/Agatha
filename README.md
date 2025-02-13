<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Para Meu Amor</title>
    <style>
        body {
            text-align: center;
            background-color: black;
            color: white;
            font-family: Arial, sans-serif;
        }
        h1 {
            font-size: 2.5em;
        }
        #countdown {
            font-size: 2em;
            margin: 20px 0;
        }
        #fireworks {
            position: fixed;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            pointer-events: none;
        }
        img {
            width: 300px;
            border-radius: 15px;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Faltam <span id="countdown"></span> para nossos 3 meses!</h1>
    <p>Meu amor, cada dia ao seu lado é um presente. Te amo demais! ❤️</p>
    <img src="sua-imagem.jpg" alt="Nossa foto juntos">
    <canvas id="fireworks"></canvas>
    
    <script>
        function updateCountdown() {
            const targetDate = new Date("2025-02-24T00:00:00").getTime();
            const now = new Date().getTime();
            const timeLeft = targetDate - now;
            
            const days = Math.floor(timeLeft / (1000 * 60 * 60 * 24));
            document.getElementById("countdown").innerText = `${days} dias`;
        }
        setInterval(updateCountdown, 1000);
        updateCountdown();
    
        const canvas = document.getElementById("fireworks");
        const ctx = canvas.getContext("2d");
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        const fireworks = [];
        
        function Firework(x, y) {
            this.x = x;
            this.y = y;
            this.radius = 2;
            this.color = `hsl(${Math.random() * 360}, 100%, 50%)`;
            this.velocity = {
                x: (Math.random() - 0.5) * 6,
                y: (Math.random() - 0.5) * 6
            };
            this.alpha = 1;
        }
        Firework.prototype.update = function() {
            this.x += this.velocity.x;
            this.y += this.velocity.y;
            this.alpha -= 0.02;
        };
        Firework.prototype.draw = function() {
            ctx.globalAlpha = this.alpha;
            ctx.beginPath();
            ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
            ctx.fillStyle = this.color;
            ctx.fill();
            ctx.globalAlpha = 1;
        };
        function createFirework() {
            for (let i = 0; i < 30; i++) {
                fireworks.push(new Firework(window.innerWidth / 2, window.innerHeight / 2));
            }
        }
        function animate() {
            requestAnimationFrame(animate);
            ctx.fillStyle = "rgba(0, 0, 0, 0.2)";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            fireworks.forEach((fw, i) => {
                fw.update();
                fw.draw();
                if (fw.alpha <= 0) fireworks.splice(i, 1);
            });
        }
        setInterval(createFirework, 500);
        animate();
    </script>
</body>
</html>

