<template>
  <span class="typewriter">
    {{ displayed }}<span v-if="!done" class="cursor">|</span>
  </span>
</template>

<script setup>
import { ref, watch, onUnmounted } from 'vue'

const props = defineProps({
  text: { type: String, required: true },
  started: { type: Boolean, default: false },
  speed: { type: Number, default: 38 },
})

const displayed = ref('')
const done = ref(false)
let timer = null

function startTyping() {
  let i = 0
  displayed.value = ''
  done.value = false
  timer = setInterval(() => {
    if (i < props.text.length) {
      displayed.value += props.text[i++]
    } else {
      done.value = true
      clearInterval(timer)
    }
  }, props.speed)
}

watch(
  () => props.started,
  (val) => { if (val) startTyping() },
  { immediate: true }
)

onUnmounted(() => clearInterval(timer))
</script>

<style scoped>
.cursor {
  display: inline-block;
  animation: blink 0.75s step-end infinite;
  color: var(--blue-mid);
  font-weight: 300;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}
</style>
