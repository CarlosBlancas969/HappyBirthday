# Happy Birthday Lelita

Carta interactiva de cumpleaños para Lelita — hecha con Vue 3 + Vite.

## Requisitos

- Node.js 18+
- npm o yarn

## Instalación y uso

```bash
# Instalar dependencias
npm install

# Iniciar servidor de desarrollo
npm run dev
```

Luego abre `http://localhost:5173` en tu navegador.

## Construcción para producción

```bash
npm run build
npm run preview
```

Los archivos finales quedan en la carpeta `dist/`.

## Personalización

### Fotos de la galería
En `src/components/LetterCard.vue`, busca el arreglo `photos`. 
Puedes agregar imágenes reales reemplazando la sección `.photo-placeholder` de cada polaroid con:

```html
<img src="/tu-foto.jpg" alt="descripción" style="width:100%;height:100%;object-fit:cover;" />
```

Y coloca las fotos en la carpeta `/public/`.

### Música
El botón de música genera un acorde suave con Web Audio API. 
Para usar tu propia canción, modifica `src/components/MusicBtn.vue` con un `<audio>` tag.

### Textos de la carta
Edita el arreglo `messages` en `src/components/LetterCard.vue` para cambiar los mensajes.

## Estructura del proyecto

```
birthday-lelita/
├── src/
│   ├── components/
│   │   ├── Hero.vue         # Pantalla inicial
│   │   ├── LetterCard.vue   # Carta principal
│   │   ├── Chopper.vue      # Animación SVG de Chopper
│   │   ├── TypeWriter.vue   # Efecto máquina de escribir
│   │   ├── Particles.vue    # Partículas flotantes
│   │   └── MusicBtn.vue     # Botón de música
│   ├── App.vue              # Componente raíz
│   ├── main.js              # Entry point
│   └── style.css            # Estilos globales
├── index.html
├── vite.config.js
└── package.json
```
