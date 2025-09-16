<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Presente para meu Amor</title>
<style>
  html, body {
    margin: 0;
    padding: 0;
    height: 100vh;
    height: calc(var(--vh, 1vh) * 100);
    display: flex;
    justify-content: center;
    align-items: center;
    background: linear-gradient(135deg, #ff9a9e, #fad0c4);
    font-family: 'Arial', sans-serif;
    overflow: hidden;
  }

  .container {
    text-align: center;
    background: rgba(255,255,255,0.85);
    padding: 30px;
    border-radius: 20px;
    box-shadow: 0 8px 20px rgba(0,0,0,0.2);
    z-index: 2;
    position: relative;
  }

  h1 {
    color: #e63946;
    font-size: 2rem;
    margin-bottom: 20px;
    opacity: 0;
    transform: scale(0);
    transition: transform 0.5s ease, opacity 0.5s ease;
  }

  h1.mostrar {
    opacity: 1;
    transform: scale(1);
  }

  button {
    background: #e63946;
    color: white;
    border: none;
    padding: 12px 20px;
    font-size: 1rem;
    border-radius: 10px;
    cursor: pointer;
    transition: 0.3s;
    z-index: 2;
    position: relative;
  }
  button:hover { background: #d62828; }

  .hidden { display: none; }

  img {
    margin-top: 20px;
    max-width: 80%;
    border-radius: 15px;
    box-shadow: 0 8px 15px rgba(0,0,0,0.3);
    transition: transform 0.5s ease, box-shadow 0.5s ease, opacity 0.5s ease;
    opacity: 0;
    transform: scale(0);
  }
  img.aparecer {
    opacity: 1;
    transform: scale(1);
    box-shadow: 0 12px 25px rgba(0,0,0,0.4);
  }

  .heart {
    position: fixed;
    bottom: 0;
    font-size: 2rem;
    color: #e63946;
    opacity: 0.8;
    z-index: 1;
    animation: float 5s linear infinite;
    -webkit-animation: float 5s linear infinite;
  }

  @keyframes float {
    0% { transform: translateY(0) scale(1); opacity: 1; }
    100% { transform: translateY(-100vh) scale(1.5); opacity: 0; }
  }
  @-webkit-keyframes float {
    0% { -webkit-transform: translateY(0) scale(1); opacity: 1; }
    100% { -webkit-transform: translateY(-100vh) scale(1.5); opacity: 0; }
  }

  #mensagem {
    margin-top: 15px;
    color: #e63946;
    font-weight: bold;
  }
</style>
</head>
<body>

<div class="container">
  <h1 id="euTeAmo">Eu te amo ❤️</h1>
  <button onclick="mostrarFrase()">Clique para o presente</button>
  <p id="mensagem"></p>
  <div id="presente" class="hidden">
    <img src="amor.jpg" alt="Presente Romântico">
  </div>
</div>

<script>
function atualizarVH() {
  let vh = window.innerHeight * 0.01;
  document.documentElement.style.setProperty('--vh', `${vh}px`);
}
window.addEventListener('resize', atualizarVH);
atualizarVH();

// Frases que vão aparecendo a cada clique
const mensagens = [
  "Hmm... ainda não! 💕",
  "Quase lá... espere mais um pouquinho! 💖",
  "Agora sim! Pronta para a surpresa? ❤️",
  "TE AMO!!!! ❤️"
];

let cliques = 0;
let coracaoInterval = null;

function mostrarFrase() {
  const p = document.getElementById('mensagem');
  const h1 = document.getElementById('euTeAmo');
  const img = document.getElementById('presente').querySelector('img');

  cliques++;

  if (cliques < mensagens.length) {
    p.textContent = mensagens[cliques-1];
  } else {
    // Última frase
    p.textContent = mensagens[mensagens.length-1];

    // Mostra "Eu te amo" animado
    h1.classList.add('mostrar');

    // Explode em corações
    setTimeout(() => {
      criarExplosao(20); // explosão inicial
      h1.style.opacity = 0;

      // Mostra imagem do presente
      document.getElementById('presente').classList.remove('hidden');
      img.classList.add('aparecer');

      // Começa corações contínuos
      if (!coracaoInterval) coracaoInterval = setInterval(criarCoracao, 1000);
    }, 800);
  }
}

// Explosão inicial de corações
function criarExplosao(qtd) {
  for (let i=0;i<qtd;i++){
    const coracao = document.createElement("div");
    coracao.classList.add("heart");
    coracao.textContent = "❤️";
    coracao.style.left = Math.random()*100 + "vw";
    coracao.style.bottom = "0";
    coracao.style.animationDuration = (2 + Math.random()*1.5) + "s";
    document.body.appendChild(coracao);
    setTimeout(()=>coracao.remove(),3000);
  }
}

// Corações contínuos
function criarCoracao() {
  const coracao = document.createElement("div");
  coracao.classList.add("heart");
  coracao.textContent = "❤️";
  coracao.style.left = Math.random()*100 + "vw";
  coracao.style.animationDuration = (4 + Math.random()*2) + "s";
  coracao.style.webkitAnimationDuration = coracao.style.animationDuration;
  document.body.appendChild(coracao);
  setTimeout(()=>coracao.remove(),5000);
}
</script>

</body>
</html>
