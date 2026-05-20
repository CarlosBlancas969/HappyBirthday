<template>
  <canvas ref="canvas" class="particles-canvas" />
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const canvas = ref(null)
let animId = null
let particles = []

function initParticles(w, h) {
  particles = Array.from({ length: 38 }, () => ({
    x: Math.random() * w,
    y: Math.random() * h,
    r: Math.random() * 3 + 1,
    dx: (Math.random() - 0.5) * 0.4,
    dy: -(Math.random() * 0.5 + 0.2),
    alpha: Math.random() * 0.5 + 0.2,
    type: Math.random() > 0.6 ? 'star' : 'circle',
    pulse: Math.random() * Math.PI * 2,
  }))
}

function drawStar(ctx, x, y, r, alpha) {
  ctx.save()
  ctx.globalAlpha = alpha
  ctx.fillStyle = '#d4a840'
  ctx.translate(x, y)
  ctx.beginPath()
  for (let i = 0; i < 5; i++) {
    const angle = (i * 4 * Math.PI) / 5 - Math.PI / 2
    const ir = (i * 4 * Math.PI) / 5 + (2 * Math.PI) / 5 - Math.PI / 2
    if (i === 0) ctx.moveTo(Math.cos(angle) * r, Math.sin(angle) * r)
    else ctx.lineTo(Math.cos(angle) * r, Math.sin(angle) * r)
    ctx.lineTo(Math.cos(ir) * (r * 0.45), Math.sin(ir) * (r * 0.45))
  }
  ctx.closePath()
  ctx.fill()
  ctx.restore()
}

function animate() {
  const c = canvas.value
  if (!c) return
  const ctx = c.getContext('2d')
  ctx.clearRect(0, 0, c.width, c.height)

  particles.forEach((p) => {
    p.x += p.dx
    p.y += p.dy
    p.pulse += 0.02
    const pulsed = p.alpha + Math.sin(p.pulse) * 0.15

    if (p.y < -10) {
      p.y = c.height + 10
      p.x = Math.random() * c.width
    }
    if (p.x < -10) p.x = c.width + 10
    if (p.x > c.width + 10) p.x = -10

    if (p.type === 'star') {
      drawStar(ctx, p.x, p.y, p.r + 1, Math.max(0, Math.min(1, pulsed)))
    } else {
      ctx.save()
      ctx.globalAlpha = Math.max(0, Math.min(1, pulsed))
      const colors = ['#b8d4e8', '#f0d8d0', '#c8d8c0', '#e8c870']
      ctx.fillStyle = colors[Math.floor(Math.random() * colors.length) % colors.length]
      // pick stable color per particle
      ctx.fillStyle = p.color || (p.color = colors[Math.floor(Math.random() * colors.length)])
      ctx.beginPath()
      ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2)
      ctx.fill()
      ctx.restore()
    }
  })

  animId = requestAnimationFrame(animate)
}

function resize() {
  const c = canvas.value
  if (!c) return
  c.width = window.innerWidth
  c.height = window.innerHeight
  initParticles(c.width, c.height)
}

onMounted(() => {
  resize()
  window.addEventListener('resize', resize)
  animate()
})

onUnmounted(() => {
  window.removeEventListener('resize', resize)
  if (animId) cancelAnimationFrame(animId)
})
</script>

<style scoped>
.particles-canvas {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 0;
}
</style>
