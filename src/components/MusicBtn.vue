<template>
  <button class="music-btn" @click="toggle" :aria-label="playing ? 'Silenciar' : 'Reproducir música'">
    <component :is="playing ? Volume2 : VolumeX" :size="16" />
    <span>{{ playing ? 'Música' : 'Música' }}</span>
    <span class="music-bars" v-if="playing">
      <span v-for="i in 3" :key="i" class="bar" :style="{ '--i': i }" />
    </span>
  </button>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Volume2, VolumeX } from 'lucide-vue-next'

const playing = ref(false)
let audio = null

onMounted(() => {
  audio = new Audio('/cancion.mp3')
  audio.loop = true
  audio.volume = 0.4

  const startAudio = () => {
    audio.play()
    playing.value = true
    document.removeEventListener('click', startAudio)
    document.removeEventListener('touchstart', startAudio)
  }

  document.addEventListener('click', startAudio)
  document.addEventListener('touchstart', startAudio)
})

function toggle() {
  if (!audio) return
  if (!playing.value) {
    audio.play()
    playing.value = true
  } else {
    audio.pause()
    playing.value = false
  }
}
</script>

<style scoped>
.music-btn {
  position: fixed;
  bottom: 1.5rem;
  right: 1.2rem;
  z-index: 100;
  display: flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.55rem 1rem;
  background: white;
  border: 1.5px solid var(--blue-soft);
  border-radius: 999px;
  color: var(--blue-ink);
  font-family: 'Crimson Pro', serif;
  font-size: 0.8rem;
  cursor: pointer;
  box-shadow: 0 4px 16px var(--shadow-blue);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.music-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 24px var(--shadow-blue);
}

.music-bars {
  display: flex;
  align-items: flex-end;
  gap: 2px;
  height: 14px;
}

.bar {
  display: block;
  width: 3px;
  background: var(--blue-mid);
  border-radius: 2px;
  animation: barDance 0.8s ease-in-out infinite;
  animation-delay: calc(var(--i) * 0.12s);
}

.bar:nth-child(1) { height: 6px; }
.bar:nth-child(2) { height: 12px; }
.bar:nth-child(3) { height: 8px; }

@keyframes barDance {
  0%, 100% { transform: scaleY(1); }
  50% { transform: scaleY(0.4); }
}
</style>