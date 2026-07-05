# Tarjetas de presentación del hero — guía de reemplazo

> Este documento es independiente del `README.md` principal del proyecto. Vive aparte para no interferir con la brújula general del proyecto. Sirve solo para un caso puntual: **reemplazar las tarjetas de presentación (`hero-id-card-light.webp` / `hero-id-card-dark.webp`) que van dentro de `.hero__panel-wrap`, en lugar del `.glass-panel` original.**

## Contexto

Las tarjetas se generan como imagen con fondo recortado (PNG con transparencia real, editado en Photoshop) y luego se convierten a WebP para el sitio. El problema recurrente: al subir la imagen a un chat (Claude, WhatsApp, etc.) para pedir ayuda, el previsualizador compone la imagen sobre fondo blanco para mostrarla en pantalla — **eso es solo la vista previa, no significa que el archivo perdió la transparencia**. El archivo real conserva su canal alfa intacto salvo que se guarde/exporte mal en algún paso intermedio (por eso siempre conviene que quien procese el archivo verifique el canal alfa por código, no a simple vista).

## Especificación técnica de salida

- Formato: **WebP**, modo **RGBA** (canal alfa preservado, sin aplanar sobre blanco ni ningún otro color).
- Peso objetivo: **≤ 100 KB por archivo**.
- Resolución: mantener la resolución original de la tarjeta entregada, salvo indicación contraria.
- Nomenclatura: `hero-id-card-light.webp` (modo diurno) y `hero-id-card-dark.webp` (modo nocturno).
- Verificación obligatoria antes de entregar: confirmar por código (no visualmente) que las esquinas de la imagen tienen alfa = 0 y el área de la tarjeta tiene alfa = 255, para garantizar que el recorte no se perdió en el proceso.

## Prompt reutilizable

Copiar y pegar este texto junto con las dos imágenes nuevas (light y dark) cada vez que haya que reemplazar las tarjetas:

```
Te adjunto las dos nuevas tarjetas de presentación (modo claro y modo oscuro) para el hero
de mi sitio ETEXCA, siguiendo la misma especificación del archivo HERO-ID-CARDS.md del repo:

- Verifica por código que el canal alfa está intacto (esquinas en 0, tarjeta en 255) antes de
  procesar. Si el chat las muestra con borde blanco, ignóralo: es solo la vista previa.
- Comprime a WebP en modo RGBA, sin aplanar el fondo, apuntando a 100 KB o menos por archivo.
- Nómbralas hero-id-card-light.webp y hero-id-card-dark.webp.
- Confirma el peso final y el estado del canal alfa de cada archivo antes de entregármelas.
```

## Historial de referencia

- Primera versión generada: tarjetas con foto de ingeniero + datos de contacto de ejemplo, comprimidas de ~1.1 MB a 93.1 KB (light) y 72.4 KB (dark) en calidad WebP 72, sin pérdida visible de transparencia.
