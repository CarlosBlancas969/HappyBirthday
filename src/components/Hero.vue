<template>
  <section class="hero">
    <!-- ── Guirnalda de banderines mejorada ── -->
    <div class="bunting">
      <svg class="bunting-svg" viewBox="0 0 800 110" xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="none">
        <!-- Cuerdas -->
        <path d="M0 22 Q200 55 400 28 Q600 2 800 22" fill="none" stroke="rgba(255,255,255,0.7)" stroke-width="2.5"/>
        <path d="M0 27 Q200 60 400 33 Q600 7 800 27" fill="none" stroke="rgba(255,255,255,0.3)" stroke-width="1.5"/>
        <!-- Banderines – fila principal, más grandes -->
        <polygon points="22,23 44,23 33,58" fill="#f5c842"/>
        <text x="33" y="47" text-anchor="middle" font-size="13" font-family="serif" fill="#1a3a6a" font-weight="bold">H</text>

        <polygon points="68,30 90,30 79,65" fill="#ff6b9d"/>
        <text x="79" y="54" text-anchor="middle" font-size="13" font-family="serif" fill="white" font-weight="bold">A</text>

        <polygon points="114,36 136,36 125,71" fill="#7ab3e8"/>
        <text x="125" y="60" text-anchor="middle" font-size="13" font-family="serif" fill="white" font-weight="bold">P</text>

        <polygon points="160,34 182,34 171,69" fill="#98e8b0"/>
        <text x="171" y="58" text-anchor="middle" font-size="13" font-family="serif" fill="#1a3a6a" font-weight="bold">P</text>

        <polygon points="206,30 228,30 217,65" fill="#f5c842"/>
        <text x="217" y="54" text-anchor="middle" font-size="13" font-family="serif" fill="#1a3a6a" font-weight="bold">Y</text>

        <!-- espacio -->
        <polygon points="264,25 286,25 275,60" fill="#ff9f7a"/>
        <text x="275" y="49" text-anchor="middle" font-size="13" font-family="serif" fill="white" font-weight="bold">B</text>

        <polygon points="310,23 332,23 321,58" fill="#c4aee8"/>
        <text x="321" y="47" text-anchor="middle" font-size="13" font-family="serif" fill="white" font-weight="bold">I</text>

        <polygon points="356,21 378,21 367,56" fill="#7ab3e8"/>
        <text x="367" y="45" text-anchor="middle" font-size="13" font-family="serif" fill="white" font-weight="bold">R</text>

        <polygon points="402,20 424,20 413,55" fill="#f5c842"/>
        <text x="413" y="44" text-anchor="middle" font-size="13" font-family="serif" fill="#1a3a6a" font-weight="bold">T</text>

        <polygon points="448,20 470,20 459,55" fill="#ff6b9d"/>
        <text x="459" y="44" text-anchor="middle" font-size="13" font-family="serif" fill="white" font-weight="bold">H</text>

        <polygon points="494,21 516,21 505,56" fill="#98e8b0"/>
        <text x="505" y="45" text-anchor="middle" font-size="13" font-family="serif" fill="#1a3a6a" font-weight="bold">D</text>

        <polygon points="540,23 562,23 551,58" fill="#c4aee8"/>
        <text x="551" y="47" text-anchor="middle" font-size="13" font-family="serif" fill="white" font-weight="bold">A</text>

        <polygon points="586,25 608,25 597,60" fill="#ff9f7a"/>
        <text x="597" y="49" text-anchor="middle" font-size="13" font-family="serif" fill="white" font-weight="bold">Y</text>

        <!-- Lelita -->
        <polygon points="644,23 666,23 655,58" fill="#f5c842"/>
        <text x="655" y="47" text-anchor="middle" font-size="13" font-family="serif" fill="#1a3a6a" font-weight="bold">L</text>

        <polygon points="690,22 712,22 701,57" fill="#7ab3e8"/>
        <text x="701" y="46" text-anchor="middle" font-size="13" font-family="serif" fill="white" font-weight="bold">E</text>

        <polygon points="736,23 758,23 747,58" fill="#ff6b9d"/>
        <text x="747" y="47" text-anchor="middle" font-size="13" font-family="serif" fill="white" font-weight="bold">!</text>

        <polygon points="778,25 800,25 789,60" fill="#98e8b0"/>
        <text x="789" y="49" text-anchor="middle" font-size="14" font-family="serif" fill="#1a3a6a">✦</text>
      </svg>
    </div>

    <div class="hero-bg">
      <div class="blob blob-1" />
      <div class="blob blob-2" />
      <div class="blob blob-3" />
    </div>

    <!-- Confeti decorativo estático -->
    <div class="confetti-deco">
      <div v-for="i in 22" :key="i" class="confetti-piece" :style="getConfettiStyle(i)" />
    </div>

    <!-- CHOPPER - izquierda (imagen real) -->
    <div class="deco-character deco-left">
      <img src="/chopper.png" alt="Chopper" class="char-img char-chopper" />
      <div class="char-label">Chopper</div>
    </div>

    <!-- SNOOPY - derecha (imagen real) -->
    <div class="deco-character deco-right">
      <img src="/snoopy1.png" alt="Snoopy" class="char-img char-snoopy" />
      <div class="char-label">Snoopy</div>
    </div>

    <div class="hero-content">
      <div class="age-badge">
        <Star :size="12" />
        <span>22</span>
        <Star :size="12" />
      </div>

      <h1 class="hero-title">
        <span class="line-1 animated-line">Happy Birthday</span>
        <span class="line-2 animated-line">Lelita</span>
      </h1>

      <div class="cake-icon">
        <BirthdayCake />
      </div>

      <p class="hero-sub">
        Programé esto porque un simple feliz cumpleaños
        <br />no era suficiente
        <Flame :size="14" class="inline-icon" />
      </p>

      <button class="open-btn" @click="$emit('open')">
        <Gift :size="16" />
        <span>Abre la sorpresa Lelita</span>
        <ChevronDown :size="16" class="bounce" />
      </button>
    </div>
  </section>
</template>

<script setup>
import BirthdayCake from './BirthdayCake.vue'
import { Star, Gift, ChevronDown, Flame } from 'lucide-vue-next'
defineEmits(['open'])

function getConfettiStyle(i) {
  const colors = ['#f5c842','#7ab3e8','#ff6b9d','#98e8b0','#c4aee8','#ff9f7a','#b8d4f0','#ffd6e0']
  const size = 6 + (i % 5) * 3
  return {
    left: ((i * 37 + 11) % 95) + '%',
    top: ((i * 23 + 7) % 85) + '%',
    width: size + 'px',
    height: size + 'px',
    background: colors[i % colors.length],
    borderRadius: i % 3 === 0 ? '50%' : '2px',
    transform: `rotate(${i * 23}deg)`,
    animationDelay: (i * 0.3) + 's',
    animationDuration: (3 + i % 4) + 's',
  }
}
</script>

<style scoped>
.hero {
  min-height: 100dvh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
  background: linear-gradient(160deg, #0d2a5e 0%, #1a4b8f 35%, #2a6abf 65%, #4a90d9 100%);
}

/* ── Guirnalda ── */
.bunting {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 3;
  pointer-events: none;
}
.bunting-svg {
  width: 100%;
  height: 110px;
  animation: buntingSway 5s ease-in-out infinite;
  filter: drop-shadow(0 4px 12px rgba(0,0,0,0.3));
}
@keyframes buntingSway {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(6px); }
}

/* ── Confeti ── */
.confetti-deco {
  position: absolute;
  inset: 0;
  pointer-events: none;
  z-index: 0;
}
.confetti-piece {
  position: absolute;
  opacity: 0.65;
  animation: confettiDrift ease-in-out infinite alternate;
}
@keyframes confettiDrift {
  0% { transform: translateY(0px) rotate(0deg); opacity: 0.45; }
  100% { transform: translateY(-14px) rotate(30deg); opacity: 0.85; }
}

/* ── Blobs ── */
.hero-bg { position: absolute; inset: 0; pointer-events: none; }
.blob {
  position: absolute;
  border-radius: 50%;
  filter: blur(70px);
  opacity: 0.3;
}
.blob-1 {
  width: 500px; height: 500px;
  background: radial-gradient(circle, #2a6abf, #0d2a5e);
  top: -100px; left: -120px;
  animation: blobFloat 8s ease-in-out infinite;
}
.blob-2 {
  width: 350px; height: 350px;
  background: radial-gradient(circle, #4a90d9, #1a4b8f);
  bottom: -80px; right: -100px;
  animation: blobFloat 10s ease-in-out infinite reverse;
}
.blob-3 {
  width: 250px; height: 250px;
  background: radial-gradient(circle, #7ab3e8, #2a6abf);
  top: 40%; right: 12%;
  animation: blobFloat 12s ease-in-out infinite 2s;
}
@keyframes blobFloat {
  0%, 100% { transform: translate(0,0) scale(1); }
  33% { transform: translate(20px,-15px) scale(1.05); }
  66% { transform: translate(-10px,10px) scale(0.97); }
}

/* ── Personajes flotando por toda la pantalla ── */
.deco-character {
  position: absolute;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.3rem;
  z-index: 2;
  pointer-events: none;
}
.deco-left {
  left: 5%;
  top: 30%;
  animation: chopperDance 2.4s ease-in-out infinite, floatAround1 8s ease-in-out infinite;
}
.deco-right {
  right: 5%;
  top: 20%;
  animation: snoopyDance 2.8s ease-in-out infinite 0.4s, floatAround2 10s ease-in-out infinite;
}
.char-img {
  width: 190px;
  height: auto;
  filter: drop-shadow(0 8px 24px rgba(0,40,120,0.45));
  mix-blend-mode: screen;
  background: transparent;
}
.char-label {
  font-family: 'Crimson Pro', serif;
  font-size: 0.65rem;
  font-style: italic;
  color: rgba(255,255,255,0.7);
  letter-spacing: 0.08em;
}

@keyframes chopperDance {
  0%   { transform: translateY(0px) rotate(-3deg); }
  25%  { transform: translateY(-16px) rotate(3deg); }
  50%  { transform: translateY(-8px) rotate(-2deg); }
  75%  { transform: translateY(-18px) rotate(4deg); }
  100% { transform: translateY(0px) rotate(-3deg); }
@keyframes floatAround1 {
  0%   { transform: translate(0px, 0px); }
  20%  { transform: translate(30px, -40px); }
  40%  { transform: translate(-20px, -80px); }
  60%  { transform: translate(50px, -30px); }
  80%  { transform: translate(-30px, 20px); }
  100% { transform: translate(0px, 0px); }
}
@keyframes floatAround2 {
  0%   { transform: translate(0px, 0px); }
  25%  { transform: translate(-40px, 50px); }
  50%  { transform: translate(20px, 100px); }
  75%  { transform: translate(-60px, 30px); }
  100% { transform: translate(0px, 0px); }
}
}
@keyframes snoopyDance {
  0%   { transform: translateY(0px) rotate(2deg); }
  30%  { transform: translateY(-14px) rotate(-3deg); }
  60%  { transform: translateY(-6px) rotate(3deg); }
  80%  { transform: translateY(-16px) rotate(-2deg); }
  100% { transform: translateY(0px) rotate(2deg); }
}

/* ── Contenido central ── */
.hero-content {
  position: relative;
  z-index: 1;
  text-align: center;
  padding: 6rem 1.5rem 2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.2rem;
}
.age-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  background: rgba(255,255,255,0.15);
  border: 1.5px solid rgba(255,255,255,0.4);
  backdrop-filter: blur(6px);
  border-radius: 999px;
  padding: 0.35rem 1rem;
  color: white;
  font-size: 0.85rem;
  letter-spacing: 0.1em;
  animation: fadeDown 0.8s ease 0.2s both;
}
.age-badge span { font-weight: 700; font-size: 1rem; }

.hero-title {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0;
  line-height: 1.1;
}
.line-1 {
  font-family: 'Crimson Pro', serif;
  font-size: clamp(1.6rem, 6vw, 2.8rem);
  font-weight: 300;
  font-style: italic;
  color: rgba(255,255,255,0.85);
  letter-spacing: 0.05em;
  animation: fadeDown 0.8s ease 0.4s both;
}
.line-2 {
  font-family: 'DM Serif Display', serif;
  font-size: clamp(3.5rem, 15vw, 7rem);
  font-weight: 400;
  letter-spacing: -0.02em;
  animation: fadeDown 0.8s ease 0.6s both;
  color: white;
  text-shadow:
    0 0 60px rgba(122,179,232,0.6),
    0 4px 30px rgba(0,30,80,0.5);
}
.cake-icon { animation: fadeDown 0.8s ease 0.7s both; }

.hero-sub {
  font-family: 'Crimson Pro', serif;
  font-size: clamp(1rem, 3.5vw, 1.25rem);
  color: rgba(255,255,255,0.82);
  font-style: italic;
  max-width: 340px;
  line-height: 1.6;
  animation: fadeDown 0.8s ease 0.9s both;
}
.inline-icon {
  display: inline-block;
  vertical-align: middle;
  color: #f5c842;
}

.open-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  margin-top: 0.5rem;
  padding: 0.9rem 2rem;
  background: white;
  color: #1a4b8f;
  border: none;
  border-radius: 999px;
  font-family: 'Crimson Pro', serif;
  font-size: 1.1rem;
  font-style: italic;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.2s ease, box-shadow 0.2s ease, background 0.2s ease, color 0.2s ease;
  box-shadow: 0 4px 24px rgba(0,30,80,0.4);
  animation: fadeDown 0.8s ease 1.1s both;
}
.open-btn:hover {
  background: #f5c842;
  color: #1a2a4a;
  transform: translateY(-3px);
  box-shadow: 0 10px 36px rgba(0,30,80,0.5);
}
.open-btn:active { transform: translateY(0); }

.bounce { animation: bounceY 1.5s ease-in-out infinite; }
@keyframes bounceY {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(4px); }
}
@keyframes fadeDown {
  from { opacity: 0; transform: translateY(-15px); }
  to { opacity: 1; transform: translateY(0); }
}

@media (max-width: 520px) {
  .char-img { width: 72px; }
  .deco-left { left: 0; bottom: 4%; }
  .deco-right { right: 0; bottom: 4%; }
  .bunting-svg { height: 70px; }
}


</style>
