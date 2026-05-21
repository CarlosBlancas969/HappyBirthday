<template>
  <article class="letter-page">
    <!-- Decorative tape pieces -->
    <div class="tape tape-top-left" />
    <div class="tape tape-top-right" />
    <div class="tape tape-bottom" />

    <!-- Paper texture lines -->
    <div class="paper-lines" aria-hidden="true">
      <div v-for="i in 18" :key="i" class="paper-line" />
    </div>

    <!-- Header of letter -->
    <div class="letter-header">
      <div class="letter-date">
        <Calendar :size="13" />
        <span>{{ currentDate }}</span>
      </div>
      <div class="letter-to">
        <Heart :size="13" />
        <span>Para Lelita, con mucho cariño</span>
      </div>
    </div>

    <!-- Chopper float -->
    <div class="chopper-section reveal" ref="chopperRef">
      <Chopper />
      <p class="chopper-caption">
        <Anchor :size="11" />
        Es un chopper ( intente dibujarlo xd )
        <Anchor :size="11" />
      </p>
    </div>

    <!-- Snoopy derecha arriba -->
    <div class="snoopy-deco snoopy-top">
      <img src="/snoopy2.png" alt="" class="snoopy-img" />
    </div>

    <!-- Message blocks -->
    <div class="messages">
      <div
          v-for="(msg, i) in messages"
          :key="i"
          class="msg-block reveal"
          :ref="el => msgRefs[i] = el"
          :style="{ '--delay': i * 0.12 + 's' }"
      >
        <div class="msg-deco">
          <component :is="msg.icon" :size="15" />
        </div>
        <p class="msg-text" :class="{ typed: msg.typed }">
          <TypeWriter v-if="msg.typed" :text="msg.text" :started="visibleMsgs[i]" />
          <template v-else>{{ msg.text }}</template>
        </p>
      </div>
    </div>



    <!-- Galería -->
    <div class="gallery-section reveal" ref="galleryRef">
      <div class="gallery-title">
        <Camera :size="15" />
        <span>Nuestros momentos</span>
        <Camera :size="15" />
      </div>

      <div class="polaroid-row">
        <div
            v-for="(photo, i) in photosRow1"
            :key="'r1-'+i"
            class="polaroid"
            :style="{ '--rot': photo.rot, '--delay': i * 0.12 + 's' }"
        >
          <div class="polaroid-img">
            <img :src="photo.src" :alt="photo.caption" class="polaroid-photo" />
          </div>
          <div class="polaroid-tape" />
          <p class="polaroid-caption">{{ photo.caption }}</p>
        </div>
      </div>

      <div class="polaroid-row">
        <div
            v-for="(photo, i) in photosRow2"
            :key="'r2-'+i"
            class="polaroid"
            :style="{ '--rot': photo.rot, '--delay': (i * 0.12 + 0.6) + 's' }"
        >
          <div class="polaroid-img">
            <img :src="photo.src" :alt="photo.caption" class="polaroid-photo" />
          </div>
          <div class="polaroid-tape" />
          <p class="polaroid-caption">{{ photo.caption }}</p>
        </div>
      </div>

      <div class="polaroid-row">
        <div
            v-for="(photo, i) in photosRow3"
            :key="'r3-'+i"
            class="polaroid"
            :style="{ '--rot': photo.rot, '--delay': (i * 0.12 + 1.2) + 's' }"
        >
          <div class="polaroid-img">
            <img :src="photo.src" :alt="photo.caption" class="polaroid-photo" />
          </div>
          <div class="polaroid-tape" />
          <p class="polaroid-caption">{{ photo.caption }}</p>
        </div>
      </div>
    </div>

    <!-- Stickers row -->
    <div class="stickers-row">
      <div class="sticker sticker-star"><Star :size="22" /></div>
      <div class="sticker sticker-heart"><Heart :size="18" /></div>
      <div class="sticker sticker-sparkle"><Sparkles :size="20" /></div>
      <div class="sticker sticker-sun"><Sun :size="20" /></div>
      <div class="sticker sticker-heart2"><Heart :size="16" /></div>
    </div>

    <!-- Snoopy centro antes del cierre -->
    <div class="snoopy-deco snoopy-end">
      <img src="/snoopy2.png" alt="" class="snoopy-img" />
    </div>

    <!-- Closing -->
    <div class="letter-close reveal" ref="closeRef">
      <div class="close-divider">
        <span /><Star :size="12" /><span />
      </div>
      <p class="close-wish">
        Que tengas un bonito cumpleaños , te quiero mucho Lelita&lt;3
        <Feather :size="14" class="inline-icon" />
      </p>
      <div class="signature">
        <Pen :size="14" />
        <span>By. Carlitos :3</span>
      </div>
    </div>
  </article>
</template>

<script setup>
import { ref, reactive, onMounted, onUnmounted } from 'vue'
import {
  Heart, Star, Sparkles, Sun, Camera, Calendar, Anchor,
  Feather, Pen, MessageCircle, Smile
} from 'lucide-vue-next'


onMounted(() => {
  // Espera a que cargue el componente y parsea todos los emojis
  const script = document.createElement('script')
  script.src = 'https://cdnjs.cloudflare.com/ajax/libs/twemoji/14.0.2/twemoji.min.js'
  script.onload = () => {
    twemoji.parse(document.querySelector('.polaroid-field'), {
      folder: 'svg',
      ext: '.svg'
    })
  }
  document.head.appendChild(script)
})
import Chopper from './Chopper.vue'
import TypeWriter from './TypeWriter.vue'

const currentDate = '22 de mayo de 2026'

const messages = [
  {
    text: 'Gracias por ser alguien que transmite tanta paz sin intentarlo<3',
    icon: MessageCircle,
    typed: false,
  },
  {
    text: 'Gracias por las risas, por esas que duelen y no tienen sentido pero son las mejores',
    icon: Smile,
    typed: false,
  },
  {
    text: 'Gracias por hacer que incluso los años no cambien el cariño que te tengo',
    icon: Heart,
    typed: true,
  },
  {
    text: 'Nunca olvides lo mucho que vales, incluso en los días donde tú misma no lo veas',
    icon: Star,
    typed: false,
  },
  {
    text: 'Porque simplemente me nace cuidarte y desearte cosas bonitas<3',
    icon: Sparkles,
    typed: false,
  },
]

const allPhotos = [
  { src: '/foto1.jpg',  caption: 'Nuestras clasesitas en Fa3 🥲',          rot: '-4deg' },
  { src: '/foto2.jpg',  caption: 'Nuestra primera salida ❤️',               rot: '3deg'  },
  { src: '/foto3.jpg',  caption: 'noche de cine 🍿',                        rot: '-2deg' },
  { src: '/foto4.jpg',  caption: 'en el KFC 🍟',                            rot: '5deg'  },
  { src: '/foto5.jpg',  caption: 'momento miope 👓',                        rot: '-3deg' },
  { src: '/foto6.jpg',  caption: 'Ni se como sobrevivi 🍽️',                rot: '4deg'  },
  { src: '/foto7.jpg',  caption: 'Lelita Piciosa 💙',                       rot: '-6deg' },
  { src: '/foto8.jpg',  caption: 'Un besito 💚',                            rot: '2deg'  },
  { src: '/foto9.jpg',  caption: 'Despues de 2 años sin vernos xd 💫',     rot: '-3deg' },
  { src: '/foto10.jpg', caption: 'Un bigotes 🍔',                           rot: '6deg'  },
  { src: '/foto11.jpg', caption: 'La conversacion que tuvimos xd 😂',       rot: '-5deg' },
  { src: '/foto12.jpg', caption: 'tarde linda, un bigotes ☀️',              rot: '3deg'  },
  { src: '/foto13.jpg', caption: 'Parecia vomito esa wbd ☕',               rot: '-2deg' },
  { src: '/foto14.jpg', caption: 'Un osito ✨',                             rot: '5deg'  },
  { src: '/foto15.jpg', caption: 'Mi bestie para siempre 💙',               rot: '-5deg' },
]

const photosRow1 = allPhotos.slice(0, 5)
const photosRow2 = allPhotos.slice(5, 10)
const photosRow3 = allPhotos.slice(10, 15)

const chopperRef = ref(null)
const galleryRef = ref(null)
const closeRef   = ref(null)
const msgRefs    = reactive([])
const visibleMsgs = reactive(Array(messages.length).fill(false))

let observer = null

onMounted(() => {
  observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add('visible')
            msgRefs.forEach((el, i) => {
              if (el === entry.target) visibleMsgs[i] = true
            })
          }
        })
      },
      { threshold: 0.1 }
  )

  const els = [chopperRef.value, galleryRef.value, closeRef.value]
  els.forEach((el) => el && observer.observe(el))
  msgRefs.forEach((el) => el && observer.observe(el))
})

onUnmounted(() => observer?.disconnect())
</script>

<style scoped>
.letter-page {
  position: relative;
  background: #fffef9;
  border-radius: 18px;
  padding: 2.5rem 1.8rem 3rem;
  max-width: 560px;
  margin: 0 auto;
  box-shadow:
      0 4px 6px rgba(42,32,24,0.06),
      0 12px 40px rgba(42,32,24,0.12),
      0 0 0 1px rgba(122,179,232,0.2);
  overflow: hidden;
}

.paper-lines {
  position: absolute;
  inset: 0;
  padding: 80px 0 0;
  pointer-events: none;
  z-index: 0;
}
.paper-line {
  height: 1px;
  background: rgba(122,179,232,0.2);
  margin-bottom: 28px;
}

.tape {
  position: absolute;
  background: rgba(122,179,232,0.3);
  border-radius: 3px;
  z-index: 10;
}
.tape-top-left  { width: 55px; height: 14px; top: -5px;   left: 40px;  transform: rotate(-8deg); }
.tape-top-right { width: 45px; height: 14px; top: -4px;   right: 50px; transform: rotate(6deg); }
.tape-bottom    { width: 50px; height: 14px; bottom: -4px; left: 50%;   transform: translateX(-50%) rotate(-3deg); }

.letter-header {
  position: relative; z-index: 1;
  display: flex; flex-direction: column;
  gap: 0.4rem; margin-bottom: 1.5rem;
}
.letter-date, .letter-to {
  display: flex; align-items: center; gap: 0.4rem;
  font-size: 0.8rem; font-style: italic;
}
.letter-date { color: var(--blue-mid); }
.letter-to   { color: var(--blush-mid); }
.letter-to :deep(svg) { color: #d08080; }

.chopper-section {
  position: relative; z-index: 1;
  text-align: center; margin: 1rem 0 2rem;
}
.chopper-caption {
  display: inline-flex; align-items: center; gap: 0.4rem;
  font-size: 0.75rem; color: var(--blue-mid);
  letter-spacing: 0.12em; text-transform: uppercase;
  margin-top: 0.5rem; font-style: italic;
}

/* Snoopy decorativo */
.snoopy-deco {
  position: relative;
  z-index: 1;
  margin: 0.5rem 0;
}

.snoopy-top {
  text-align: right;
  padding-right: 0.5rem;
}

.snoopy-mid {
  text-align: left;
  padding-left: 0.5rem;
}

.snoopy-end {
  text-align: center;
  margin: 1rem 0;
}

.snoopy-img {
  width: 65px;
  height: auto;
  filter: drop-shadow(0 4px 8px rgba(106,90,160,0.2));
}

.snoopy-top .snoopy-img {
  animation: snoopyBobFlip 3.5s ease-in-out infinite;
}

.snoopy-mid .snoopy-img {
  width: 60px;
  animation: snoopyBob 3.5s ease-in-out infinite 1s;
}

.snoopy-end .snoopy-img {
  width: 75px;
  animation: snoopyBob 3.5s ease-in-out infinite 0.5s;
}

@keyframes snoopyBob {
  0%, 100% { transform: translateY(0px); }
  50%       { transform: translateY(-8px); }
}

@keyframes snoopyBobFlip {
  0%, 100% { transform: scaleX(-1) translateY(0px); }
  50%       { transform: scaleX(-1) translateY(-8px); }
}

/* Messages */
.messages {
  position: relative; z-index: 1;
  display: flex; flex-direction: column;
  gap: 1.4rem; margin-bottom: 2.5rem;
}
.msg-block {
  display: flex; gap: 1rem; align-items: flex-start;
  transition-delay: var(--delay) !important;
}
.msg-deco {
  flex-shrink: 0; width: 28px; height: 28px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--blue-soft), var(--blush));
  display: flex; align-items: center; justify-content: center;
  color: var(--blue-ink);
  box-shadow: 0 2px 8px var(--shadow-blue);
  margin-top: 2px;
}
.msg-text {
  font-family: 'Crimson Pro', serif;
  font-size: clamp(1.05rem, 3.5vw, 1.2rem);
  line-height: 1.65; color: var(--text-body);
  font-style: italic;
}

/* Galería */
.gallery-section {
  position: relative; z-index: 1;
  margin-bottom: 2rem;
}
.gallery-title {
  display: flex; align-items: center;
  justify-content: center; gap: 0.5rem;
  font-size: 0.78rem; text-transform: uppercase;
  letter-spacing: 0.12em; color: var(--text-soft);
  margin-bottom: 1.4rem;
}

.polaroid-row {
  display: flex;
  gap: 0.85rem;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 1rem;
}

.polaroid {
  position: relative;
  background: white;
  padding: 0.55rem 0.55rem 2.5rem;
  box-shadow: 0 4px 16px rgba(30,77,140,0.18), 0 1px 4px rgba(0,0,0,0.1);
  transform: rotate(var(--rot));
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  cursor: default;
  animation: polaroidIn 0.6s ease var(--delay) both;
  flex-shrink: 0;
}
.polaroid:hover {
  transform: rotate(0deg) scale(1.06);
  box-shadow: 0 12px 36px rgba(30,77,140,0.3);
  z-index: 5;
}
@keyframes polaroidIn {
  from { opacity: 0; transform: rotate(var(--rot)) scale(0.82) translateY(22px); }
  to   { opacity: 1; transform: rotate(var(--rot)) scale(1) translateY(0); }
}

.polaroid-tape {
  position: absolute;
  top: -7px; left: 50%;
  transform: translateX(-50%) rotate(-2deg);
  width: 38px; height: 13px;
  background: rgba(122,179,232,0.35);
  border-radius: 2px;
}
.polaroid-img {
  width: 120px; height: 100px;
  overflow: hidden;
  background: linear-gradient(135deg, #e8f2f8, #f5e8e0);
}
.polaroid-photo {
  width: 100%; height: 100%;
  object-fit: cover; display: block;
}
.polaroid-caption {
  font-family: 'Crimson Pro', serif;
  font-size: 0.68rem; font-style: italic;
  color: var(--text-soft); text-align: center;
  position: absolute; bottom: 0.5rem;
  left: 0; right: 0;
  line-height: 1.2;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

/* Stickers */
.stickers-row {
  position: relative; z-index: 1;
  display: flex; align-items: center;
  justify-content: center; gap: 1.2rem;
  margin-bottom: 2rem; flex-wrap: wrap;
}
.sticker {
  width: 38px; height: 38px; border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  box-shadow: 0 2px 10px var(--shadow-warm);
  animation: stickerBounce 4s ease-in-out infinite;
}
.sticker-star    { background: linear-gradient(135deg, #fdeec8, #f5d890); color: var(--gold); animation-delay: 0s; }
.sticker-heart   { background: linear-gradient(135deg, #fdd8d0, #f0b8a8); color: #c07060; animation-delay: 0.3s; }
.sticker-sparkle { background: linear-gradient(135deg, #d8eef8, var(--blue-soft)); color: var(--blue-ink); animation-delay: 0.6s; }
.sticker-sun     { background: linear-gradient(135deg, #f8ecd0, #f0d898); color: #c0880a; animation-delay: 0.9s; }
.sticker-heart2  { background: linear-gradient(135deg, #d8f0d8, #b8d8b8); color: #4a8050; animation-delay: 1.2s; }
@keyframes stickerBounce {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50%       { transform: translateY(-5px) rotate(5deg); }
}

/* Closing */
.letter-close {
  position: relative; z-index: 1;
  text-align: center; display: flex;
  flex-direction: column; align-items: center; gap: 1.2rem;
}
.close-divider {
  display: flex; align-items: center; gap: 0.6rem;
  width: 100%; color: var(--gold);
}
.close-divider span {
  flex: 1; height: 1px;
  background: linear-gradient(to right, transparent, var(--gold-light), transparent);
}
.close-wish {
  font-family: 'DM Serif Display', serif;
  font-size: clamp(1.1rem, 4vw, 1.4rem);
  color: var(--dark); line-height: 1.5;
  max-width: 300px;
}
.inline-icon {
  display: inline-block; vertical-align: middle;
  color: var(--gold); margin-left: 0.2rem;
}
.signature {
  display: flex; align-items: center; gap: 0.5rem;
  font-family: 'Playfair Display', serif;
  font-size: 1rem; font-style: italic;
  color: var(--text-soft);
}

@media (max-width: 480px) {
  .polaroid-img { width: 100px; height: 90px; }
  .polaroid { padding-bottom: 1.8rem; }
  .polaroid-row { gap: 0.5rem; }
  .snoopy-img { width: 50px; }
}

/* Twemoji styling */
:deep(.polaroid-caption img.emoji) {
  width: 1em;
  height: 1em;
  vertical-align: -0.15em;
  display: inline-block;
}
</style>
