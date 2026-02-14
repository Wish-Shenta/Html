# Html
For my kuyang
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Valentine Special 💎</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;600&display=swap" rel="stylesheet">

<style>
body{
    margin:0;
    padding:0;
    background:#000;
    font-family:'Poppins',sans-serif;
    height:100vh;
    overflow:hidden;
    display:flex;
    justify-content:center;
    align-items:center;
    color:white;
}

/* Stars */
.star{
    position:absolute;
    width:2px;
    height:2px;
    background:white;
    border-radius:50%;
    animation:twinkle 2s infinite alternate;
}
@keyframes twinkle{
    from{opacity:0.2;}
    to{opacity:1;}
}

/* Card */
.card{
    background:rgba(255,255,255,0.05);
    padding:50px;
    border-radius:25px;
    text-align:center;
    backdrop-filter:blur(15px);
    box-shadow:0 0 40px rgba(255,0,128,0.5);
    z-index:2;
    max-width:400px;
}

h1{
    font-size:2.5em;
    background:linear-gradient(90deg,#ff4da6,#ff0066);
    -webkit-background-clip:text;
    -webkit-text-fill-color:transparent;
}

button{
    margin-top:15px;
    padding:10px 25px;
    border:none;
    border-radius:25px;
    background:linear-gradient(90deg,#ff4da6,#ff0066);
    color:white;
    cursor:pointer;
    transition:.3s;
    box-shadow:0 0 15px #ff0066;
}
button:hover{
    transform:scale(1.1);
}

.hidden{
    display:none;
    margin-top:15px;
}

/* Fireworks canvas */
canvas{
    position:absolute;
    top:0;
    left:0;
    pointer-events:none;
}
</style>
</head>
<body>

<canvas id="fireworks"></canvas>

<div class="card">
    <h1>Happy Valentine 💎</h1>
    <p>Untuk My Kuyangs ❤️</p>
    <p>Kamu adalah alasan senyumku ✨</p>

    <button onclick="showMessage()">Buka Pesan 💌</button>

    <div id="message" class="hidden">
        <p>Maukah kamu jadi Valentine-ku? 💖</p>
        <button onclick="accepted()">Terima 💕</button>
        <button onclick="alert('Gapapa 😆 Aku tetap doakan yang terbaik ❤️')">Tolak 😅</button>
    </div>
</div>

<audio autoplay loop>
<source src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_115b9b6d45.mp3?filename=romantic-background-112191.mp3" type="audio/mp3">
</audio>

<script>
function showMessage(){
    document.getElementById("message").style.display="block";
}

/* Stars */
for(let i=0;i<100;i++){
    let star=document.createElement("div");
    star.className="star";
    star.style.top=Math.random()*100+"vh";
    star.style.left=Math.random()*100+"vw";
    star.style.animationDuration=(Math.random()*2+1)+"s";
    document.body.appendChild(star);
}

/* Fireworks */
const canvas=document.getElementById("fireworks");
const ctx=canvas.getContext("2d");
canvas.width=window.innerWidth;
canvas.height=window.innerHeight;

let particles=[];

function accepted(){
    alert("Sekarang kamu resmi jadi Valentine-ku 💎💖");
    for(let i=0;i<5;i++){
        createFirework();
    }
}

function createFirework(){
    let x=Math.random()*canvas.width;
    let y=Math.random()*canvas.height/2;
    for(let i=0;i<50;i++){
        particles.push({
            x:x,
            y:y,
            radius:2,
            color:`hsl(${Math.random()*360},100%,60%)`,
            speedX:(Math.random()-0.5)*6,
            speedY:(Math.random()-0.5)*6,
            life:100
        });
    }
}

function animate(){
    requestAnimationFrame(animate);
    ctx.fillStyle="rgba(0,0,0,0.2)";
    ctx.fillRect(0,0,canvas.width,canvas.height);

    particles.forEach((p,index)=>{
        p.x+=p.speedX;
        p.y+=p.speedY;
        p.life--;
        ctx.beginPath();
        ctx.arc(p.x,p.y,p.radius,0,Math.PI*2);
        ctx.fillStyle=p.color;
        ctx.fill();
        if(p.life<=0){
            particles.splice(index,1);
        }
    });
}
animate();
</script>

</body>
</html>
