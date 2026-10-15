<div align="center">

# ☀️ Luzka — Monitor UV

### Aplicación web progresiva (PWA) de monitoreo del Índice UV en tiempo real  
### con análisis biofacial y recomendaciones personalizadas de fotoprotección

<br/>

![Versión](https://img.shields.io/badge/versión-1.0.0-7B1D3A?style=for-the-badge)
![PWA](https://img.shields.io/badge/PWA-Instalable-F5A07A?style=for-the-badge&logo=pwa)
![API](https://img.shields.io/badge/API-OpenUV-3B9EC4?style=for-the-badge)
![Licencia](https://img.shields.io/badge/licencia-MIT-F5ECD7?style=for-the-badge&labelColor=7B1D3A)
![Universidad](https://img.shields.io/badge/UPCH-Ingeniería_Industrial-7B1D3A?style=for-the-badge)

<br/>

> *Desarrollado como proyecto académico en la Facultad de Ingeniería Industrial · Universidad Peruana Cayetano Heredia*

</div>

---

## 🌟 ¿Qué es Luzka?

**Luzka** es una aplicación web móvil instalable que combina dos tecnologías para proteger tu piel del sol:

1. **Sensor biofacial** — analiza el color de piel del usuario mediante la cámara del dispositivo y lo clasifica según la Escala de Fitzpatrick (Tipos I–VI).
2. **Índice UV en tiempo real** — consulta la API de OpenUV con las coordenadas GPS del usuario y cruza ese dato con el tipo de piel detectado para generar **recomendaciones personalizadas de fotoprotección**.

---

## 🎨 Paleta de colores institucional

| Nombre | Hex | Uso |
|--------|-----|-----|
| 🟥 Guinda | `#7B1D3A` | Color primario, encabezados, botones principales |
| 🍑 Durazno | `#F5A07A` | Acentos, íconos, gradientes |
| 🥛 Crema | `#F5ECD7` | Fondos, superficies claras |
| 🩵 Celeste | `#3B9EC4` | Botones de GPS, elementos de ubicación |

---

## ✨ Funcionalidades

### 🔬 Análisis Biofacial
- Acceso a la cámara frontal del dispositivo
- Captura del color promedio del pixel central del video
- Clasificación automática en la **Escala de Fitzpatrick** (I–II, III–IV, V–VI)
- Fallback simulado si la cámara no está disponible

### 📍 Geolocalización Inteligente
- Detección automática de ubicación vía GPS del navegador
- **Mapa interactivo** con OpenStreetMap + Leaflet.js (sin costo, sin API key)
- **Dirección legible** (calle, barrio, ciudad) via geocodificación inversa con Nominatim
- Pin personalizado en colores institucionales UPCH, movible con clic

### ☀️ Índice UV en Tiempo Real
- Consulta a la **API de OpenUV** con coordenadas precisas
- Clasificación según estándares OMS (Bajo → Extremo)
- Escala visual de riesgo UV con gradiente de color
- Curva estimada del día (hora pico de radiación)
- Datos de ozono estratosférico

### 💊 Recomendaciones Personalizadas
Cada usuario recibe consejos adaptados al **cruce de su tipo de piel + índice UV actual**:
- 🧴 Factor de protección solar recomendado (FPS 15 / 30 / 50+)
- 🧢 Uso de sombrero de ala ancha
- 🕶️ Lentes UV400
- 💧 Hidratación según nivel de radiación
- ⏰ Tiempo máximo de exposición sin protección

### 📱 PWA — Instalable
- Funciona como app nativa en Android, iOS y escritorio
- Botón de instalación nativo (`beforeinstallprompt`)
- Service Worker con caché offline
- `manifest.json` con tema en colores UPCH
- Respeta `prefers-reduced-motion` del sistema

### 🌐 Bilingüe
- Interfaz completa en **Español / English**
- Toggle de idioma disponible en todas las pantallas

---

## 🗂️ Estructura del proyecto

```
luzka/
│
├── index.html        ← App completa (HTML + CSS + JS en un solo archivo)
├── manifest.json     ← Configuración PWA (nombre, íconos, colores)
└── sw.js             ← Service Worker (caché offline, estrategia Cache-first)
```

> ⚠️ Los tres archivos deben estar en la **misma carpeta raíz** del servidor.

---

## 🚀 Despliegue con GitHub Pages

1. Sube los 3 archivos a la raíz de tu repositorio en GitHub
2. Ve a **Settings → Pages → Source → Deploy from branch**
3. Selecciona `main` → `/ (root)` → **Save**
4. En ~2 minutos tu app estará en:

```
https://milena2708.github.io/LUSKA-app/
```

> La app requiere **HTTPS** para que funcionen la cámara y el GPS. GitHub Pages lo provee automáticamente. ✅

---

## 🔑 Configuración de la API

La API key de OpenUV está definida como constante en `index.html`:

```js
const OPENUV_API_KEY = 'openuv-c74mrmuao0w3s-io';
const API_BASE       = 'https://api.openuv.io/api/v1/uv';
```

El plan gratuito de OpenUV incluye **250 consultas/día**. Si el límite se alcanza, la app muestra un mensaje amigable con código HTTP 403.

Regístrate o gestiona tu clave en: [openuv.io](https://www.openuv.io)

---

## 🛠️ Tecnologías utilizadas

| Tecnología | Versión | Propósito |
|------------|---------|-----------|
| HTML5 nativo | — | Estructura y semántica |
| JavaScript ES6+ | — | Lógica de la aplicación |
| Tailwind CSS | CDN | Estilos y diseño responsivo |
| Leaflet.js | 1.9.4 | Mapa interactivo |
| OpenStreetMap | — | Tiles del mapa (gratuito) |
| Nominatim | — | Geocodificación inversa (gratuito) |
| OpenUV API | v1 | Índice UV en tiempo real |
| Web APIs nativas | — | Cámara, GPS, Service Worker, PWA |
| Google Fonts | — | DM Sans + Playfair Display |

---

## 📱 Flujo de usuario

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐    ┌──────────────────┐
│   Bienvenida    │ →  │ Sensor Biofacial │ →  │  Mi Ubicación   │ →  │   Resultados     │
│                 │    │                  │    │                 │    │                  │
│  Logo Luzka     │    │  Feed cámara     │    │  Botón GPS      │    │  Índice UV       │
│  Pasos rápidos  │    │  circular        │    │  Mapa Leaflet   │    │  Escala OMS      │
│  Btn Instalar   │    │  Barra análisis  │    │  Dirección real │    │  Curva del día   │
│                 │    │  Fitzpatrick     │    │  Pin movible    │    │  Cards bienestar │
└─────────────────┘    └──────────────────┘    └─────────────────┘    └──────────────────┘
```

---

## ⚠️ Permisos requeridos

| Permiso | Para qué se usa | ¿Se almacena? |
|---------|----------------|---------------|
| 📷 Cámara | Análisis biofacial del tipo de piel | ❌ No |
| 📍 Ubicación (GPS) | Consulta del Índice UV local | ❌ No |

> Luzka **no almacena, transmite ni comparte** ningún dato personal. Todo el procesamiento ocurre localmente en el dispositivo del usuario.

---

## 👩‍💻 Autora

**Milena Nicol Yalli Espinoza** · Facultad de Ingeniería Industrial  
Universidad Peruana Cayetano Heredia (UPCH) · Lima, Perú

---

<div align="center">

Hecho con ☀️ y paleta guinda, durazno y celeste — colores UPCH

</div>
