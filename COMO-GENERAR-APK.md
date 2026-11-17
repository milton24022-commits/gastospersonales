# Cómo generar el .apk

Este entorno de Claude no tiene el SDK de Android ni acceso a los repositorios de Google/Gradle, así que no puedo compilar el .apk directamente aquí. Lo que sí dejé listo es todo lo necesario para que tú lo generes en pocos minutos, por dos caminos. Elige el que te acomode más.

---

## Opción A — Sin instalar Android Studio (la más rápida)

Usa **PWABuilder** (https://www.pwabuilder.com), una herramienta gratuita de Microsoft que empaqueta cualquier PWA (app web) en un .apk firmado y listo para instalar.

1. Sube la carpeta `gastos-app/` (con `index.html`, `manifest.json`, `sw.js` e `icons/`) a un hosting gratuito. Las dos formas más simples:
   - **GitHub Pages**: crea un repositorio en GitHub, sube estos archivos, activa Pages en Settings → Pages. Te da una URL tipo `https://tuusuario.github.io/gastos-app/`.
   - **Netlify Drop**: entra a https://app.netlify.com/drop y arrastra la carpeta. Te da una URL al instante, sin crear cuenta.
2. Entra a https://www.pwabuilder.com, pega esa URL y presiona "Start".
3. Cuando analice tu app, ve a la pestaña **Android** y presiona "Generate Package".
4. Descarga el paquete: incluye un `.apk` (o `.aab` para la Play Store) ya firmado, listo para instalar en cualquier celular Android (activa "Instalar apps de orígenes desconocidos" si tu celular lo pide).

Este camino no requiere instalar nada en tu computador.

---

## Opción B — Con Android Studio (control total del proyecto nativo)

Esta opción usa **Capacitor**, que ya dejé configurado en esta misma carpeta (`package.json`, `capacitor.config.json`).

### Requisitos
- Node.js instalado (https://nodejs.org)
- Android Studio instalado (https://developer.android.com/studio), con el SDK de Android configurado

### Pasos
1. Abre una terminal dentro de la carpeta `gastos-app/`.
2. Instala las dependencias:
   ```
   npm install
   ```
3. Agrega la plataforma Android y sincroniza los archivos de la app:
   ```
   npx cap add android
   npx cap sync android
   ```
   Esto crea una carpeta `android/` con un proyecto nativo completo de Android Studio.
4. Abre el proyecto en Android Studio:
   ```
   npx cap open android
   ```
5. En Android Studio, espera a que sincronice Gradle (puede tardar varios minutos la primera vez, descarga dependencias).
6. Genera el APK desde el menú: **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
7. El archivo queda en `android/app/build/outputs/apk/debug/app-debug.apk`, listo para copiar a tu celular e instalar.

> Si luego quieres publicarla en Google Play, en Android Studio usa **Build → Generate Signed Bundle / APK** para crear una versión firmada con tu propia clave.

---

## ¿Cuál elegir?

- Si solo necesitas un .apk para probar o entregar como Hito: **Opción A**, es más rápida y no requiere instalar nada.
- Si quieres seguir desarrollando funciones nativas (notificaciones, cámara, etc.) o publicarla en Google Play: **Opción B**.
