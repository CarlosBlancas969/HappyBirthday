<template>
  <div class="app">
    <Particles />
    <MusicBtn />

    <Transition name="fade" mode="out-in">
      <Hero v-if="!opened" @open="handleOpen" key="hero" />

      <main v-else class="letter-wrapper" key="letter">
        <!-- Guirnalda -->
        <div class="bunting">
          <svg class="bunting-svg" viewBox="0 0 800 110" xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="none">
            <path d="M0 22 Q200 55 400 28 Q600 2 800 22" fill="none" stroke="rgba(255,255,255,0.7)" stroke-width="2.5"/>
            <path d="M0 27 Q200 60 400 33 Q600 7 800 27" fill="none" stroke="rgba(255,255,255,0.3)" stroke-width="1.5"/>
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

        <!-- Confeti -->
        <div class="confetti-deco">
          <div v-for="i in 22" :key="i" class="confetti-piece" :style="getConfettiStyle(i)" />
        </div>

        <div class="letter-inner">
          <header class="page-header">
            <div class="header-tag">
              <Star :size="11" />
              <span>22 años</span>
              <Star :size="11" />
            </div>
            <h2 class="page-title">Una carta para ti</h2>
            <p class="page-subtitle">de parte de alguien que se alegra de que existas</p>
          </header>

          <LetterCard />

          <button class="back-btn" @click="opened = false">← Volver</button>

          <footer class="page-footer">
            <p>
              <Heart :size="13" />
              Hecho con cariño
              <Heart :size="13" />
            </p>
          </footer>
        </div>
      </main>
    </Transition>

    <canvas ref="confettiCanvas" class="confetti-canvas" />
  </div>
</template>

<script setup>
import { ref, nextTick } from 'vue'
import { Star, Heart } from 'lucide-vue-next'
import Particles from './components/Particles.vue'
import Hero from './components/Hero.vue'
import LetterCard from './components/LetterCard.vue'
import MusicBtn from './components/MusicBtn.vue'

const opened = ref(false)
const confettiCanvas = ref(null)

function handleOpen() {
  opened.value = true
  nextTick(() => {
    burstConfetti()
    setTimeout(() => {
      window.scrollTo({ top: 0, behavior: 'instant' })
    }, 50)
  })
}

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

function burstConfetti() {
  const canvas = confettiCanvas.value
  if (!canvas) return
  canvas.width = window.innerWidth
  canvas.height = window.innerHeight
  const ctx = canvas.getContext('2d')
  const pieces = Array.from({ length: 90 }, () => ({
    x: Math.random() * canvas.width,
    y: -20,
    r: Math.random() * 8 + 3,
    dx: (Math.random() - 0.5) * 4,
    dy: Math.random() * 4 + 2,
    alpha: 1,
    color: ['#f5c842','#7ab3e8','#ff6b9d','#98e8b0','#c4aee8','#ff9f7a'][Math.floor(Math.random()*6)],
    spin: Math.random() * Math.PI,
    dspin: (Math.random() - 0.5) * 0.15,
  }))

  let frame = 0
  const max = 180

  function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height)
    pieces.forEach(p => {
      p.x += p.dx
      p.y += p.dy
      p.dy += 0.04
      p.spin += p.dspin
      p.alpha = Math.max(0, 1 - frame / max)
      ctx.save()
      ctx.globalAlpha = p.alpha
      ctx.fillStyle = p.color
      ctx.translate(p.x, p.y)
      ctx.rotate(p.spin)
      ctx.fillRect(-p.r / 2, -p.r / 2, p.r, p.r * 0.5)
      ctx.restore()
    })
    frame++
    if (frame < max) requestAnimationFrame(draw)
    else ctx.clearRect(0, 0, canvas.width, canvas.height)
  }
  draw()
}
</script>

<style scoped>
.app {
  min-height: 100dvh;
  position: relative;
}

.confetti-canvas {
  position: fixed;
  top: 0; left: 0;
  width: 100%; height: 100%;
  pointer-events: none;
  z-index: 50;
}

.letter-wrapper {
  min-height: 100dvh;
  background: linear-gradient(160deg, #0d2a5e 0%, #1a4b8f 35%, #2a6abf 65%, #4a90d9 100%);
  padding: 2rem 1rem 4rem;
  position: relative;
  z-index: 1;
}

.letter-inner {
  max-width: 560px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.page-header {
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.6rem;
  padding-top: 5rem;
}

.header-tag {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  background: rgba(255,255,255,0.15);
  border: 1.5px solid rgba(255,255,255,0.35);
  border-radius: 999px;
  padding: 0.3rem 0.9rem;
  font-size: 0.75rem;
  color: white;
  letter-spacing: 0.1em;
  box-shadow: 0 2px 10px rgba(0,0,0,0.2);
  animation: fadeDown 0.6s ease both;
}

.page-title {
  font-family: 'DM Serif Display', serif;
  font-size: clamp(2rem, 7vw, 3rem);
  color: white;
  line-height: 1.1;
  animation: fadeDown 0.6s ease 0.15s both;
}

.page-subtitle {
  font-family: 'Crimson Pro', serif;
  font-size: clamp(0.9rem, 3vw, 1.05rem);
  color: rgba(255,255,255,0.75);
  font-style: italic;
  animation: fadeDown 0.6s ease 0.3s both;
}

.page-footer {
  text-align: center;
  padding-bottom: 2rem;
  font-family: 'Crimson Pro', serif;
  font-size: 0.85rem;
  font-style: italic;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.4rem;
  color: rgba(255,255,255,0.6);
}

.page-footer :deep(svg) { color: #ff6b9d; }

@keyframes fadeDown {
  from { opacity: 0; transform: translateY(-12px); }
  to { opacity: 1; transform: translateY(0); }
}

.back-btn {
  position: fixed;
  top: 1rem;
  left: 1rem;
  z-index: 999;
  background: white;
  color: #1a4b8f;
  border: none;
  border-radius: 999px;
  padding: 0.5rem 1.2rem;
  font-family: 'Crimson Pro', serif;
  font-size: 1rem;
  cursor: pointer;
  box-shadow: 0 4px 16px rgba(0,30,80,0.2);
}
.back-btn:hover { background: #f5c842; }

.bunting {
  position: fixed;
  top: 0; left: 0;
  width: 100%;
  z-index: 10;
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

.confetti-deco {
  position: fixed;
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

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.6s ease, transform 0.6s ease;
}
.fade-enter-from {
  opacity: 0;
  transform: translateY(20px);
}
.fade-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}


</style>