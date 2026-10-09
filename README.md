# ANDRÉSELIZALDE — Nexus Experiments

**Un pequeño universo de juegos, retos de IQ y cultura general dedicado a Andrés Elizalde.**

La primera experiencia es **El Espiral de Andrés**: un explorador matemático del conjunto de Mandelbrot, con geometría auténtica y una dirección artística psicodélica, inspirado libremente en descripciones de efectos visuales asociados con *Nexus / 2C-B*. Ninguna sustancia interviene; es una obra digital, no una simulación científica de los efectos de una droga.

![Vista de Nexus en un móvil](assets/preview.png)

## Abrir desde el celular

En cuanto se cree el repositorio público `jfcarpiopuntocom/andreselizalde` y se habilite GitHub Pages (Settings → Pages → Deploy from a branch → `main` → `/ (root)`), la URL esperada será:

**https://jfcarpiopuntocom.github.io/andreselizalde/**

La URL de arriba es la **dirección prevista**, no una dirección publicada ni verificada todavía.

**Compatibilidad objetivo:** Safari en iPhone 14 en adelante; Chrome/Firefox/Edge recientes en Android y desktop. WebGL utiliza la GPU, con alternativa de renderizado 2D por Web Worker. No usa frameworks externos, módulos JavaScript, fuentes descargadas, rastreadores ni llamadas a API.

## Controles

- Un toque sobre el fractal: ampliar donde toques.
- Arrastrar: recorrer el conjunto.
- Pellizcar con dos dedos: zoom continuo. También funcionan rueda del ratón y los botones `+` y `−`.
- Seis portales: El espiral, El universo, Caballitos, Tres cuerpos, Abismo doble y Mini universo.
- **Pausar**: detener deformaciones y cambios cromáticos.
- **Mandala**: simetría radial de ocho segmentos, disponible cuando hay WebGL.
- **Viaje**: exploración autónoma lenta, disponible cuando hay WebGL.
- Intensidad, detalle, captura PNG, ficha informativa y movimiento reducido.

El renderizador de GPU usa dos pasadas: fractal Mandelbrot fuera de pantalla y composición animada en pantalla. El cálculo CPU recupera precisión en niveles de acercamiento que exceden las posibilidades prácticas de `float` en el shader. El modo CPU aprovecha un `Worker` para no ocupar el hilo de la interfaz, con anulación de cálculos obsoletos.

## Arquitectura y archivos

```text
andreselizalde/
├── index.html         ← la experiencia inicial / entrada GitHub Pages
├── styles.css         ← interfaz móvil / safe areas / horizontal
├── app.js             ← interacción, GPU WebGL, efectos, fallback
├── cpu-worker.js      ← Mandelbrot CPU original adaptado
├── standalone.html     ← edición autónoma de un solo archivo
├── assets/            ← favicon y captura de referencia
├── juegos/            ← próximos juegos
├── iq/                ← próximos tests y acertijos de IQ
├── cultura-general/   ← próximos cuestionarios
├── tests/             ← pruebas automatizadas y manuales
└── .github/workflows/ ← comprobación de integridad
```

El proyecto es **HTML5 + CSS3 + JavaScript + WebGL1**. No requiere Node para ejecutarse ni instala `three.js`: el shader WebGL directo consume menos recursos, evita dependencias CDN y funciona en Safari móvil sin build step. No hay servidor de backend.

## Ejecutar localmente

```bash
python3 -m http.server 8000
# abrir http://localhost:8000
```

Para compartir un solo archivo también está `standalone.html` (incluye CSS, JavaScript y el código del worker dentro del HTML). O simplemente publicar todos los archivos en un hosting HTTPS que respete las rutas relativas. El worker puede estar restringido en `file://`, por lo que se recomienda HTTP local o HTTPS.

## Verificar

```bash
node --check app.js
node --check cpu-worker.js
node --test tests/static.test.mjs
```

Las pruebas funcionales de navegador están en `tests/smoke.py` (requieren Python, Playwright y Chromium; `pip install playwright`). La evidencia manual de WebGL y Canvas 2D se hizo con Chromium, no con un iPhone físico; el dispositivo real sigue pendiente de validación en Safari.

## Sensibilidad visual y rigor

El usuario puede pausar o reducir el movimiento. Se respeta la preferencia `prefers-reduced-motion`; no se diseñaron destellos estroboscópicos. La imagen es una **interpretación artística**, no una representación universal de fenómenos subjetivos.

Referencia descriptiva: [PsychonautWiki, 2C-B, Visual effects](https://psychonautwiki.org/wiki/2C-B). Matemáticas: [Mandelbrot set](https://en.wikipedia.org/wiki/Mandelbrot_set).

**Creado para Andrés, de J. F. Carpio.**