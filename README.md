<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday!</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;600&display=swap" rel="stylesheet">
    <style>
        body, html {
            margin: 0;
            padding: 0;
            height: 100%;
            font-family: 'Poppins', sans-serif;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: #1e1e1e;
            overflow: hidden;
        }
        h1 {
            font-size: 4rem;
            color: #ff69b4;
            text-align: center;
            animation: fadeIn 2s ease-in-out;
        }
        p {
            font-size: 1.5rem;
            color: #fff;
            text-align: center;
            max-width: 600px;
            animation: fadeIn 3s ease-in-out;
        }
        .container {
            text-align: center;
            position: relative;
        }
        canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
        }
        @keyframes fadeIn {
            0% { opacity: 0; }
            100% { opacity: 1; }
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Happy Birthday, anu 🎉</h1>
        <p>Wishing you endless happiness, laughter, and love on your special day. You are a true gem! 💖</p>
    </div>

    <canvas id="confetti"></canvas>

    <script>
        // Confetti Effect
        var canvas = document.getElementById("confetti");
        var context = canvas.getContext("2d");
        var confettiPieces = [];

        function randomRange(min, max) {
            return Math.random() * (max - min) + min;
        }

        function ConfettiPiece() {
            this.x = Math.random() * canvas.width;
            this.y = Math.random() * canvas.height - canvas.height;
            this.color = `hsl(${randomRange(0, 360)}, 100%, 50%)`;
            this.size = randomRange(5, 10);
            this.speed = randomRange(1, 5);
        }

        ConfettiPiece.prototype.update = function() {
            this.y += this.speed;
            if (this.y > canvas.height) {
                this.y = -this.size;
            }
        };

        ConfettiPiece.prototype.draw = function() {
            context.fillStyle = this.color;
            context.fillRect(this.x, this.y, this.size, this.size);
        };

        function init() {
            for (var i = 0; i < 200; i++) {
                confettiPieces.push(new ConfettiPiece());
            }
        }

        function animate() {
            context.clearRect(0, 0, canvas.width, canvas.height);
            for (var i = 0; i < confettiPieces.length; i++) {
                confettiPieces[i].update();
                confettiPieces[i].draw();
            }
            requestAnimationFrame(animate);
        }

        window.addEventListener('resize', function() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        init();
        animate();
    </script>
</body>
</html>
