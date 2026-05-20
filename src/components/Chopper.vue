<template>
  <div class="chopper-wrap">
    <div class="chopper-shadow" />
    <svg
      class="chopper"
      viewBox="0 0 120 160"
      xmlns="http://www.w3.org/2000/svg"
    >
      <!-- Hat brim -->
      <ellipse cx="60" cy="38" rx="44" ry="12" fill="#e03030" />
      <!-- Hat top -->
      <rect x="30" y="8" width="60" height="32" rx="8" fill="#e03030" />
      <!-- Hat band pink -->
      <rect x="28" y="30" width="64" height="10" rx="4" fill="#f7b3b3" />
      <!-- Hat cross -->
      <rect x="55" y="10" width="10" height="28" rx="3" fill="#f7b3b3" />
      <rect x="44" y="20" width="32" height="10" rx="3" fill="#f7b3b3" />

      <!-- Ears -->
      <ellipse cx="22" cy="62" rx="14" ry="18" fill="#f5dfc0" />
      <ellipse cx="98" cy="62" rx="14" ry="18" fill="#f5dfc0" />
      <ellipse cx="22" cy="62" rx="8" ry="12" fill="#e8c4a0" />
      <ellipse cx="98" cy="62" rx="8" ry="12" fill="#e8c4a0" />

      <!-- Face -->
      <ellipse cx="60" cy="80" rx="36" ry="38" fill="#f5dfc0" />

      <!-- Eyes -->
      <ellipse cx="46" cy="72" rx="9" ry="10" fill="white" />
      <ellipse cx="74" cy="72" rx="9" ry="10" fill="white" />
      <circle cx="48" cy="73" r="5" fill="#3a2a1a" />
      <circle cx="76" cy="73" r="5" fill="#3a2a1a" />
      <circle cx="50" cy="71" r="1.8" fill="white" />
      <circle cx="78" cy="71" r="1.8" fill="white" />

      <!-- Nose -->
      <ellipse cx="60" cy="84" rx="7" ry="5" fill="#e8a880" />

      <!-- Mouth smile -->
      <path d="M 50 94 Q 60 103 70 94" stroke="#c07050" stroke-width="2.5" fill="none" stroke-linecap="round" />

      <!-- Cheek blush -->
      <ellipse cx="38" cy="88" rx="9" ry="6" fill="#f0a090" opacity="0.5" />
      <ellipse cx="82" cy="88" rx="9" ry="6" fill="#f0a090" opacity="0.5" />

      <!-- Body -->
      <ellipse cx="60" cy="130" rx="28" ry="26" fill="#7aaec8" />

      <!-- Hooves / arms -->
      <ellipse cx="32" cy="120" rx="10" ry="8" fill="#3a2a1a" transform="rotate(-20,32,120)" />
      <ellipse cx="88" cy="120" rx="10" ry="8" fill="#3a2a1a" transform="rotate(20,88,120)" />

      <!-- Tummy -->
      <ellipse cx="60" cy="132" rx="16" ry="14" fill="#f5dfc0" />

      <!-- Legs -->
      <ellipse cx="48" cy="152" rx="9" ry="8" fill="#3a2a1a" />
      <ellipse cx="72" cy="152" rx="9" ry="8" fill="#3a2a1a" />
    </svg>

    <!-- Sparkles around chopper -->
    <div class="sparkle s1"><Sparkles :size="14" /></div>
    <div class="sparkle s2"><Star :size="10" /></div>
    <div class="sparkle s3"><Sparkles :size="11" /></div>
    <div class="sparkle s4"><Star :size="9" /></div>
  </div>
</template>

<script setup>
import { Sparkles, Star } from 'lucide-vue-next'
</script>

<style scoped>
.chopper-wrap {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: flex-end;
  width: 160px;
  height: 190px;
  margin: 0 auto;
}

.chopper {
  width: 120px;
  height: 160px;
  animation: chopperFloat 4s ease-in-out infinite;
  filter: drop-shadow(0 8px 16px rgba(74, 134, 168, 0.3));
  position: relative;
  z-index: 1;
}

.chopper-shadow {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 70px;
  height: 12px;
  background: radial-gradient(ellipse, rgba(74,134,168,0.25) 0%, transparent 70%);
  border-radius: 50%;
  animation: shadowPulse 4s ease-in-out infinite;
}

@keyframes chopperFloat {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-14px); }
}

@keyframes shadowPulse {
  0%, 100% { transform: translateX(-50%) scaleX(1); opacity: 0.6; }
  50% { transform: translateX(-50%) scaleX(0.75); opacity: 0.3; }
}

.sparkle {
  position: absolute;
  color: var(--gold);
  animation: sparklePop 3s ease-in-out infinite;
}

.s1 { top: 15px; left: 8px; animation-delay: 0s; }
.s2 { top: 5px; right: 20px; animation-delay: 0.7s; }
.s3 { bottom: 30px; right: 5px; animation-delay: 1.4s; }
.s4 { bottom: 50px; left: 15px; animation-delay: 2.1s; }

@keyframes sparklePop {
  0%, 100% { opacity: 0; transform: scale(0.5); }
  50% { opacity: 1; transform: scale(1); }
}
</style>
