 # ➰PÁGINA DE REDIRECIONAMENTO➰
- 💎 Me Chamo Kaio.
- ✔ Sou designer gráfico, a mais de 2 anos, nesse tempo todo já fiz diversa arte, desde logos ate flyers.

 ## ➰CONTATO➰

-  <a href="https://www.youtube.com/seu-canal-youtube-aqui" target="_blank"><img src="https://img.shields.io/badge/YouTube-FF0000?style=for-the-   badge&logo=youtube&logoColor=white" target="_blank"></a>
- <a href="https://instagram.com/seu-usuário-instagram-aqui" target="_blank"><img src="https://img.shields.io/badge/-Instagram-%23E4405F?style=for-the-   badge&logo=instagram&logoColor=white" target="_blank"></a> 
- MY STORE https://sites.google.com/view/kaiogsdesigner/home


### ➰ALGUMAS ARTES➰

<div>
<img src="https://user-images.githubusercontent.com/103225660/166126918-aaaf4fbd-3733-4fa8-9124-3936be3db4ea.png" width="320" height="320"/>
  <img src="https://user-images.githubusercontent.com/103225660/166127267-4f4883c0-9d5e-4e57-ae1a-435fef485919.jpg" width="320" height="320"/>
    <img src="https://user-images.githubusercontent.com/103225660/166127280-d50bfc3f-7109-4837-b6ba-af1a5222a6a0.png" width="320" height="320"/>
      <img src="https://user-images.githubusercontent.com/103225660/166127305-511e2935-275c-4cfb-a44c-484a94c7d50d.png" width="320" height="320"/>
    <img src="https://user-images.githubusercontent.com/103225660/166127956-7c261e7e-902e-492e-b5bb-6944191debe8.png" width="320" height="320"/>
  <img src="https://user-images.githubusercontent.com/103225660/166127327-313d48f2-462c-4608-9dd5-6eca7fea4f48.png" width="320" height="320"/>
<div>

### Copiar os Códgos:
 
 ````
  //variáveis da bolinha
let xBolinha = 300;
let yBolinha = 200;
let dBolinha = 30
let raio = dBolinha / 2;

//velocidade da bolinha
let velocidadeXBolinha = 6;
let velocidadeYBolinha = 6;
let raqueteComprimento = 10;
let raqueteAltura = 90;

//variáveis da raquete
let xRaquete = 5;
let yRaquete = 150;

//variáveis do oponente
let xRaqueteOponente = 585;
let yRaqueteOponente = 150;
let velocidadeYOponente;

//placar do jogo
let meusPontos = 0;
let pontosOponete = 0;
let colidiu = false;

// sons do jogo
let raquetada;
let pontos;
let trilha;

function preload() {
  trilha = loadSound("trilha.mp3");
  ponto = loadSound("ponto.mp3");
  raquetada = loadSound("raquetada.mp3");
}

function setup() {
  createCanvas(600, 400);
  trilha.loop();
}

function draw() {
  background(255);
  meiodojogo();
  mostraBolinha();
  mostraBolinha();
  movimentaBolinha();
  verificaColisaoBorda();
  mostraRaquete(xRaquete, yRaquete);
  movimentaMinhaRaquete();
  //verificaColisaoRaquete();
  colisaoMinhaRaqueteBiblioteca();
  mostraRaquete();
  mostraRaqueteOponente();
  movimentaRaqueteOpoenete();
  colisaoRaqueteOponenteBiblioteca();
  incluiPlacar();
  marcaPontos();
}

function meiodojogo() {
  fill(color(135, 0, 0));
  rect(300, 0, 5, 800);
}

function mostraBolinha() {
  fill(45);
  circle(xBolinha, yBolinha, dBolinha);
}

function movimentaBolinha() {
  xBolinha += velocidadeXBolinha;
  yBolinha += velocidadeYBolinha;
}

function verificaColisaoBorda() {
  if (xBolinha + raio > width || xBolinha - raio < 0) {
    velocidadeXBolinha *= -1;
  }
  if (yBolinha + raio > height || yBolinha - raio < 0) {
    velocidadeYBolinha *= -1;
  }
}

function mostraRaquete(x, y) {
  stroke(255, 48, 48);
  fill(color(255, 48, 18));
  rect(x, y, raqueteComprimento, raqueteAltura);
}

function mostraRaqueteOponente() {
  stroke(48, 152, 255);
  fill(color(48, 152, 255));
  rect(xRaqueteOponente, yRaqueteOponente, raqueteComprimento, raqueteAltura);
}

function movimentaMinhaRaquete() {
  if (keyIsDown(87)) {
    yRaquete -= 10;
  }
  if (keyIsDown(83)) {
    yRaquete += 10;
  }
}

function verificaColisaoRaquete() {
  if (
    xBolinha - raio < xRaquete + raqueteComprimento &&
    yBolinha - raio < yRaquete + raqueteAltura &&
    yBolinha + raio > yRaquete
  ) {
    velocidadeXBolinha *= -1;
  }
}

function colisaoMinhaRaqueteBiblioteca() {
  colidiu = collideRectCircle(
    xRaquete,
    yRaquete,
    raqueteComprimento,
    raqueteAltura,
    xBolinha,
    yBolinha,
    raio
  );
  if (colidiu) {
    velocidadeXBolinha *= -1;
    raquetada.play();
  }
}

function colisaoRaqueteOponenteBiblioteca() {
  colidiu = collideRectCircle(
    xRaqueteOponente,
    yRaqueteOponente,
    raqueteComprimento,
    raqueteAltura,
    xBolinha,
    yBolinha,
    raio
  );
  if (colidiu) {
    velocidadeXBolinha *= -1;
    raquetada.play();
  }
}

function movimentaRaqueteOpoenete() {
  if (keyIsDown(UP_ARROW)) {
    yRaqueteOponente -= 10;
  }
  if (keyIsDown(DOWN_ARROW)) {
    yRaqueteOponente += 10;
  }
}

function incluiPlacar() {
  stroke(255);
  textAlign(CENTER);
  textSize(16);
  fill(color(255, 140, 0));
  rect(255, 0, 40, 20);
  fill(255);
  text(meusPontos, 275, 15);
  fill(color(255, 140, 0));
  rect(310, 0, 40, 20);
  fill(255);
  text(pontosOponete, 330, 15);
}

function marcaPontos() {
  if (xBolinha > 585) {
    meusPontos += 1;
    ponto.play();
  }

  if (xBolinha < 15) {
    pontosOponete += 1;
    ponto.play();
  }
}

 ````


