<template>
  <div class="cake-wrap">
    <!-- Velas -->
    <div class="candles-row">
      <div
          v-for="(c, i) in candles"
          :key="i"
          class="candle-wrap"
          :style="{ '--ci': i, '--cx': c.x + '%' }"
      >
        <div class="flame-wrap" :class="{ lit: flamesOn }">
          <div class="flame-outer" />
          <div class="flame-inner" />
          <div class="flame-shine" />
        </div>
        <div class="candle" :style="{ background: c.color }" />
      </div>
    </div>

    <!-- Pisos del pastel -->
    <div
        v-for="(tier, i) in tiers"
        :key="i"
        class="tier-wrap"
        :class="{ dropped: tiersDropped[i] }"
        :style="{ '--ti': i }"
    >
      <!-- Crema ondulada encima de cada piso -->
      <svg class="cream-svg" viewBox="0 0 200 22" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg">
        <path
            d="M0 14 Q12 2 25 14 Q38 2 50 14 Q62 2 75 14 Q88 2 100 14 Q112 2 125 14 Q138 2 150 14 Q162 2 175 14 Q188 2 200 14 L200 22 L0 22 Z"
            fill="#f5f0ff"
        />
        <path
            d="M0 14 Q12 2 25 14 Q38 2 50 14 Q62 2 75 14 Q88 2 100 14 Q112 2 125 14 Q138 2 150 14 Q162 2 175 14 Q188 2 200 14"
            fill="none" stroke="#e0d0f8" stroke-width="1.5"
        />
      </svg>

      <!-- Cuerpo del piso -->
      <div class="tier-body" :style="{ background: tier.bg, width: tier.w, height: tier.h }">
        <!-- Decoraciones -->
        <div class="tier-decos">
          <div
              v-for="j in tier.dots"
              :key="j"
              class="deco-dot"
              :style="{ left: (j / (tier.dots + 1) * 100) + '%', background: tier.dotColor }"
          />
        </div>
        <!-- Número 22 en el piso base -->
        <div v-if="i === tiers.length - 1" class="tier-number">22</div>
      </div>

      <!-- Franja inferior del piso -->
      <div class="tier-band" :style="{ background: tier.band, width: tier.w }" />
    </div>

    <!-- Plato -->
    <div class="plate" :class="{ visible: tiersDropped[tiers.length - 1] }" />

    <!-- Caption -->
    <p class="cake-caption" :class="{ visible: flamesOn }">
      <Sparkles :size="11" />
      Feliz cumpleaños Lelita
      <Sparkles :size="11" />
    </p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Sparkles } from 'lucide-vue-next'

const candles = [
  { x: 28, color: '#c4aee8' },
  { x: 50, color: '#a8c4e8' },
  { x: 72, color: '#b8d4c0' },
]

const tiers = [
  {
    w: '120px', h: '52px',
    bg: 'linear-gradient(180deg, #b8cce8 0%, #a0b8dc 100%)',
    band: 'linear-gradient(90deg, #8aabda, #7a9bca)',
    dots: 3, dotColor: '#f0ebff',
  },
  {
    w: '160px', h: '58px',
    bg: 'linear-gradient(180deg, #c4aee8 0%, #b090d8 100%)',
    band: 'linear-gradient(90deg, #9a78c8, #8a68b8)',
    dots: 4, dotColor: '#f0ebff',
  },
  {
    w: '200px', h: '62px',
    bg: 'linear-gradient(180deg, #a8bce0 0%, #90a8d0 100%)',
    band: 'linear-gradient(90deg, #7890c0, #6880b0)',
    dots: 5, dotColor: '#e8d8ff',
  },
]

const tiersDropped = ref([false, false, false])
const flamesOn = ref(false)

onMounted(() => {
  // Cada piso cae con delay escalonado
  tiers.forEach((_, i) => {
    setTimeout(() => {
      tiersDropped.value[i] = true
    }, 400 + i * 500)
  })
  // Las velas se encienden al final
  setTimeout(() => {
    flamesOn.value = true
  }, 400 + tiers.length * 500 + 300)
})
</script>

<style scoped>
.cake-wrap {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0;
  padding: 1rem 0 0.5rem;
  position: relative;
}

/* ── Velas ── */
.candles-row {
  display: flex;
  justify-content: center;
  gap: 0;
  position: relative;
  width: 120px;
  height: 52px;
  margin-bottom: -2px;
  z-index: 10;
}

.candle-wrap {
  position: absolute;
  left: var(--cx);
  bottom: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  transform: translateX(-50%);
}

.candle {
  width: 10px;
  height: 28px;
  border-radius: 4px 4px 2px 2px;
  box-shadow: inset 1px 0 0 rgba(255,255,255,0.3);
}

.flame-wrap {
  position: relative;
  width: 16px;
  height: 24px;
  margin-bottom: 2px;
  opacity: 0;
  transform: scaleY(0);
  transform-origin: bottom center;
  transition: opacity 0.4s ease calc(var(--ci) * 0.15s),
  transform 0.4s cubic-bezier(0.34,1.56,0.64,1) calc(var(--ci) * 0.15s);
}

.flame-wrap.lit {
  opacity: 1;
  transform: scaleY(1);
}

.flame-outer {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 14px;
  height: 22px;
  background: radial-gradient(ellipse at 50% 80%, #f5c842 30%, #f08020 70%, transparent 100%);
  border-radius: 50% 50% 30% 30%;
  animation: flicker 1.8s ease-in-out infinite;
}

.flame-inner {
  position: absolute;
  bottom: 4px;
  left: 50%;
  transform: translateX(-50%);
  width: 7px;
  height: 12px;
  background: radial-gradient(ellipse at 50% 80%, #fff8e0 40%, #fde080 100%);
  border-radius: 50% 50% 30% 30%;
  animation: flicker 1.8s ease-in-out infinite 0.2s;
}

.flame-shine {
  position: absolute;
  bottom: 8px;
  left: 50%;
  transform: translateX(-50%);
  width: 3px;
  height: 6px;
  background: white;
  opacity: 0.7;
  border-radius: 50%;
  animation: flicker 2.2s ease-in-out infinite 0.1s;
}

@keyframes flicker {
  0%, 100% { transform: translateX(-50%) scaleX(1) scaleY(1); }
  25% { transform: translateX(-52%) scaleX(0.9) scaleY(1.05); }
  50% { transform: translateX(-48%) scaleX(1.08) scaleY(0.95); }
  75% { transform: translateX(-51%) scaleX(0.95) scaleY(1.03); }
}

/* ── Pisos ── */
.tier-wrap {
  display: flex;
  flex-direction: column;
  align-items: center;
  opacity: 0;
  transform: translateY(-120px);
  transition: opacity 0.45s cubic-bezier(0.22,1,0.36,1) calc(var(--ti) * 0.08s),
  transform 0.55s cubic-bezier(0.34,1.28,0.64,1) calc(var(--ti) * 0.08s);
  z-index: calc(10 - var(--ti));
  position: relative;
}

.tier-wrap.dropped {
  opacity: 1;
  transform: translateY(0);
}

.cream-svg {
  width: 100%;
  height: 22px;
  display: block;
  margin-bottom: -1px;
  filter: drop-shadow(0 1px 2px rgba(180,160,220,0.2));
}

.tier-body {
  position: relative;
  border-radius: 4px;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

.tier-decos {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
}

.deco-dot {
  position: absolute;
  width: 9px;
  height: 9px;
  border-radius: 50%;
  top: 50%;
  transform: translateY(-50%);
  opacity: 0.75;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}

.tier-number {
  font-family: 'DM Serif Display', serif;
  font-size: 1.3rem;
  font-style: italic;
  color: rgba(255,255,255,0.85);
  letter-spacing: 0.05em;
  position: relative;
  z-index: 1;
  text-shadow: 0 1px 4px rgba(0,0,0,0.15);
}

.tier-band {
  height: 10px;
  border-radius: 0 0 6px 6px;
  margin-top: -1px;
}

/* ── Plato ── */
.plate {
  width: 220px;
  height: 14px;
  background: radial-gradient(ellipse, #e0d4f0 0%, #ccc0e0 60%, transparent 100%);
  border-radius: 50%;
  margin-top: 2px;
  opacity: 0;
  transform: scaleX(0.6);
  transition: opacity 0.5s ease, transform 0.5s cubic-bezier(0.34,1.4,0.64,1);
}

.plate.visible {
  opacity: 1;
  transform: scaleX(1);
}

/* ── Caption ── */
.cake-caption {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  font-size: 0.75rem;
  color: var(--blue-mid);
  letter-spacing: 0.12em;
  text-transform: uppercase;
  font-style: italic;
  margin-top: 0.8rem;
  opacity: 0;
  transform: translateY(8px);
  transition: opacity 0.5s ease, transform 0.5s ease;
}

.cake-caption.visible {
  opacity: 1;
  transform: translateY(0);
}
</style>