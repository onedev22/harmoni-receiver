# Harmoni Glass Cast Receiver

Un receptor Chromecast personalizado con diseño glassmorphism que refleja el estilo visual de Harmoni.

## ¿Qué es?

Este archivo HTML es la interfaz que se muestra en tu **TV o pantalla Chromecast** cuando transmites desde Harmoni. Reemplaza la UI genérica del Default Media Receiver con una pantalla hermosa que muestra:

- 🖼️ Portada del álbum con fondo desenfocado animado
- 🎵 Título y artista de la canción actual
- ⏱️ Barra de progreso en tiempo real
- 🎮 Controles de reproducción (solo visual, el control real es desde el teléfono)
- 💎 Diseño glassmorphism con blur, gradientes y animaciones

## Cómo activarlo (requiere deploy)

El Cast SDK de Google **requiere** que el receiver esté alojado en HTTPS público para poder registrar un Application ID. Hay dos opciones gratuitas:

### Opción A: GitHub Pages (recomendado)

1. Crea un repositorio en GitHub (puede ser privado)
2. Sube el archivo `index.html` en la rama `main` o en una carpeta `/docs`
3. Activa **Settings → Pages → Deploy from branch**
4. Obtendrás una URL tipo: `https://tuusuario.github.io/harmoni-receiver/`

### Opción B: Firebase Hosting

```bash
npm install -g firebase-tools
firebase login
firebase init hosting
# Copia index.html a public/index.html
firebase deploy
```

## Registrar el Application ID

1. Ve a [Google Cast SDK Developer Console](https://cast.google.com/publish/)
2. Inicia sesión con tu cuenta de Google
3. Haz clic en **Add new application**
4. Selecciona **Custom Receiver**
5. Ingresa el nombre: `Harmoni`
6. Ingresa la URL de tu hosting: `https://tuurl.github.io/index.html`
7. Obtendrás un **Application ID** (ej: `ABCD1234`)

## Registrar tu dispositivo Chromecast (solo para desarrollo)

Mientras el receiver no esté publicado (aprobado), solo funciona en dispositivos registrados:

1. En la misma consola, ve a **Cast receiver devices**
2. Agrega el **serial number** de tu Chromecast
3. Espera ~15 minutos para que se propague

## Actualizar el código Android

Una vez que tengas el Application ID, actualiza `CastOptionsProvider.kt`:

```kotlin
// app/src/main/java/com/amurayada/music/cast/CastOptionsProvider.kt
return CastOptions.Builder()
    .setReceiverApplicationId("TU_APPLICATION_ID_AQUI")
    .build()
```

## Sin Application ID (modo temporal)

Mientras no tengas el ID, el proyecto sigue usando `DEFAULT_MEDIA_RECEIVER_APPLICATION_ID` que muestra la UI genérica de Google. El receiver personalizado ya está listo para cuando lo registres.

## Personalización del receiver

El archivo `index.html` usa solo HTML5 + CSS + JavaScript puro. Puedes modificar:

- **Colores**: Las variables de `rgba()` en el CSS
- **Tipografía**: El link de Google Fonts (actualmente usa `Inter`)
- **Animaciones**: Los keyframes `pulse` y `spin`
- **Diseño**: Las dimensiones de la tarjeta `#player-card`
