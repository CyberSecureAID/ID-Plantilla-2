# ETEXCA (nombre temporal) — Sitio Web Corporativo
### Tecnología e Ingeniería de la Construcción — Canadá

> **Este documento es la brújula del proyecto.** Se construyó a partir de la plantilla JPO Contracting (construcción/ingeniería), pero el objetivo NO es reskinear esa plantilla — es construir una plataforma con estructura visual, arquitectura de componentes y lenguaje de diseño propios, coherentes con el rubro del nuevo cliente. Cualquier sesión de trabajo (yo, Claude, u otra persona) debe leer esto ANTES de tocar código, para no repetir patrones de JPO por inercia.

> **⚠️ Pivote de dirección visual (v2 "Viewport"):** el cliente pidió explícitamente abandonar la dirección editorial/documental descrita en §1 y adoptar un lenguaje **glassmorphism premium** (2026), inspirado en software BIM/CAD: fondo casi negro, paneles de cristal con blur, acento cian tecnológico + ámbar cálido, brackets de "viewport" como elemento firma, movimiento (parallax de hero, reveals con stagger). La tabla de contraste de §1 y la sección "Concepto de diseño" describen la dirección **anterior (v1, ya reemplazada)** — se conservan como historial, no como guía vigente. Ver §1-bis para el sistema actual.

---

## 1. Por qué este proyecto es distinto a JPO (y debe seguir siéndolo)

JPO Contracting es una plantilla cinematográfica de construcción/ingeniería: hero con imagen de fondo + parallax + zoom, header que se autoculta al hacer scroll, grid de cards con glassmorphism, tarjetas flip 3D, partículas en canvas, paleta dorado/azul/cian, chatbot flotante "Leo", mapa Leaflet en popover.

Nada de eso es apropiado para una firma de servicios profesionales. El objetivo explícito del cliente es que **la portada no se vea igual**, ni la estructura, ni la paleta, ni la arquitectura de secciones. Este README existe para que ese objetivo no se diluya archivo por archivo.

> **Actualización de rubro:** el cliente confirmó que ETEXCA opera en tecnología e ingeniería de la construcción (no legal/consultoría/finanzas como se asumía inicialmente). El lenguaje de diseño editorial/documental descrito abajo sigue siendo apropiado — el registro "cláusula legal" funciona igual de bien como registro "expediente técnico/ficha de proyecto" — pero el copy y los servicios listados en la sección 4 ya reflejan el rubro real.

### Concepto de diseño 2026 para servicios profesionales (investigado, no inventado)
- **Editorial, no cinematográfico**: layouts asimétricos, márgenes grandes, tipografía grande como elemento visual dominante — no imagen de fondo con parallax/zoom.
- **Secciones full-viewport que alternan claro/oscuro** (bloques de alto contraste) en vez de un scroll continuo sobre el mismo fondo.
- **Paleta contenida**: tonos profundos (marino/tinta/carbón) + un acento cálido (bronce/óxido/dorado apagado) — nada de cian ni estética Web3/gamer.
- **Movimiento sutil**, sin partículas ni efectos "cinematográficos" de fondo.
- **CTA de consulta siempre visible**, en vez de widget de chat flotante.
- **Mobile-first real**, tipografía serif o sans geométrica para transmitir autoridad y confianza.

### Tabla de contraste estructural (JPO → Nuevo sitio)
| Elemento | JPO (original) | Nuevo sitio |
|---|---|---|
| Hero | Imagen de fondo + parallax/zoom cinematográfico | Tipográfico, sin imagen grande de fondo, texto como protagonista |
| Header | Se oculta/reaparece con scroll (lógica compleja, blindada) | Fijo, minimalista, o sidebar de navegación |
| Servicios | Grid de 12 cards glassmorphism en 4 categorías | Lista editorial numerada, layout asimétrico |
| Diferenciadores | 5 tarjetas con flip 3D | Secciones full-viewport alternando fondo claro/oscuro |
| Fondo animado | Canvas de partículas conectadas | Sin canvas; micro-interacciones sutiles vía CSS |
| Asistente virtual | Chatbot flotante "Leo" con motor propio + Wikipedia + ConceptNet | Por definir — probablemente se elimina (ver sección 3) |
| Mapa | Leaflet + CARTO Dark Matter en popover del footer | Por definir — probablemente se elimina o se simplifica |
| Paleta | Dorado `#F5A800` + azul `#0A2A6E` + cian de partículas | Marino/tinta + acento bronce (a definir con cliente) |

---

## 1-bis. Sistema de diseño vigente — v2 "Viewport" (glassmorphism)

Reemplaza por completo la paleta/tipografía/estructura de v1. Motivo del cliente: quiere una página con calidad visual de producto premium (~10.000 USD), con glassmorphism, blur, animación y una portada sin franjas blancas ni overlay pesado.

- **Color**: `--void #05070D` (fondo casi negro) · `--void-soft #0A0F1C` · cristal `rgba(154,184,255,0.06–0.16)` · acento primario `--cyan #4FD8FF` (referencia a los renders wireframe de las imágenes de portada) · acento secundario `--amber #F2A93C` (referencia al mapa de Canadá iluminado en `hero-bg.webp`). Ver `css/tokens.css`.
- **Tipografía**: Space Grotesk (display, geométrica/técnica) + Inter (cuerpo) + IBM Plex Mono (etiquetas "readout").
- **Elemento firma**: brackets de esquina tipo viewport de software BIM/CAD (`.viewport` en `layout.css`) alrededor del panel del hero y del formulario de contacto — no se repite en cada tarjeta para no saturar (regla: la audacia se gasta en un solo lugar).
- **Hero**: `img` real (no `background-image`) con `object-fit:cover`, overlay direccional ligero (ya no un velo uniforme) y parallax sutil vía JS. Esto resuelve dos quejas puntuales del cliente: las franjas blancas laterales y el "velo azul horrible".
- **CTA persistente**: `.float-cta`, una píldora de cristal flotante (esquina inferior derecha) que aparece al salir del hero y se oculta cerca del formulario — reemplaza la barra de ancho completo tipo aviso de cookies que el cliente pidió eliminar.
- **Servicios**: grid de tarjetas de cristal (`service-grid`), ya no lista editorial numerada.
- **Diferenciadores**: banner full-bleed con la segunda imagen del cliente (antes solo se usaba mal, con blur pesado, en Servicios) + 3 tarjetas de eje.

### Pendiente/decisiones abiertas de v2
- [ ] Logo real: el header ya tiene una zona de logo dedicada (`.site-header__mark-glyph`), hoy con un monograma "E" de cristal como placeholder — reemplazar por `<img>` en cuanto exista logotipo.
- [ ] Confirmar si los 3 ejes de "Diferenciadores" (Ingeniería con datos / Stack digital integrado / Ejecución en obra real) reflejan la propuesta de valor real del cliente, o si debe basarse en los 5 servicios/rubro con más precisión.
- [ ] Revisar en dispositivo real que el parallax e imágenes fuente (1920×960) luzcan bien en pantallas muy verticales (recorte lateral por `object-fit:cover`, no franjas — pero vale una revisión visual).

---

## 2. Objetivo general
Construir, con el mismo nivel de ingeniería (HTML/CSS/JS vanilla, sin frameworks, arquitectura modular en archivos separados), un sitio que:
1. No se confunda visualmente con JPO ni con ninguna plantilla genérica.
2. Comunique autoridad, confianza y sobriedad — códigos visuales del sector legal/consultoría/finanzas, no de construcción.
3. Sea bilingüe (si el cliente lo confirma) reutilizando el patrón de `i18n.js` / `i18n-data.js`, pero con contenido 100% propio.
4. Sea mantenible: cada archivo con una sola responsabilidad clara, igual que en JPO.

---

## 3. Estado de la información del proyecto

### 3.1 Información del negocio
| Dato | Estado |
|---|---|
| Nombre del despacho/firma/consultora | 🟡 **Temporal: "ETEXCA"**. El cliente aún no tiene nombre definitivo — se usa como placeholder consistente en `<title>`, header, footer y meta description. Reemplazar en cuanto se confirme. |
| Especialidad exacta | 🟢 **Confirmada: tecnología e ingeniería de la construcción.** |
| Ubicación (ciudad/país) | 🟡 **Parcial: Canadá confirmado, ciudad específica pendiente.** El footer y la sección de contacto muestran solo "Canadá" por ahora. |
| Lista de servicios principales | 🟡 **Placeholder razonado.** No se recibió lista real; se listaron 5 servicios típicos de una firma de ingeniería/tecnología de la construcción de esta escala (§ 02.1–02.5 en `index.html`). El cliente debe confirmar o ajustar esta lista. |
| Datos de contacto (teléfono, email) | 🔴 **Pendientes.** El correo corporativo aún no existe (sin dominio propio todavía). El HTML deja esto explícito como "pendiente" en vez de inventar un dato — ver sección de contacto en `index.html`. |

### 3.2 Identidad visual
| Dato | Estado |
|---|---|
| Logo o manual de marca existente | 🔴 Pendiente. No confirmado si existe. |
| Paleta | 🟢 **Confirmada y construida**: ink `#0E1526` / paper `#F4F1E8` / bronze `#9C6B30` (ver `css/tokens.css`). |
| Carpeta "Imágenes" (fotos reales del cliente) | 🔴 Pendiente. `index.html` no usa imágenes reales todavía — el hero es tipográfico por diseño, así que esto ya no bloquea el hero, pero sí bloquea cualquier sección futura que las requiera. |

### 3.3 Alcance funcional
| Decisión | Estado |
|---|---|
| Chatbot | 🟢 **Resuelto: no lleva.** `.consult-bar` (CTA fija) lo reemplaza funcionalmente. |
| Mapa | 🟢 **Resuelto: no lleva por ahora.** Sin Leaflet, sin `footer-map.js`. |
| Idioma(s) del sitio | 🟢 **Resuelto: monolingüe ES por ahora.** No se implementó `i18n.js`; si se confirma bilingüe más adelante, se agrega sin romper la estructura actual. |
| Formulario de contacto | 🟡 **Estructura lista, backend pendiente.** El formulario en `index.html` tiene `action="#"` como placeholder — falta decidir a qué servicio conecta (Web3Forms, EmailJS, mailto) una vez exista el correo corporativo. |

---

## 4. Plan de archivos (referencia de JPO → estado real en el nuevo proyecto)

| Archivo JPO | Rol original | Estado en ETEXCA |
|---|---|---|
| `index.html` | Estructura completa de la página | 🟢 Construido — hero tipográfico, servicios, diferenciador, contacto. Copy real donde había datos, placeholders explícitos donde no. |
| `style.css` | Estilos hero + servicios + cards + CTA | 🟢 Reescrito y modularizado en `css/tokens.css`, `css/layout.css`, `css/header.css`, `css/components.css` — una responsabilidad por archivo. |
| `hero.css` | Estilos específicos del hero cinematográfico | ✅ Eliminado — el hero es tipográfico, sin imagen ni parallax. |
| `hero.js` | Nav scroll, hamburguesa, parallax, partículas, contadores | 🟢 Reemplazado por `js/main.js`: solo hamburguesa + reveal sutil al scroll. Sin parallax ni canvas. |
| `scroll.js` | Motor del chatbot "Leo" | ✅ No se construye — decisión tomada: sin chatbot. |
| `data.js` / `data-en.js` | Base de conocimiento del chatbot | ✅ No aplica. |
| `conceptnet-module.js` | Fallback de razonamiento conceptual del bot | ✅ No aplica. |
| `i18n.js` / `i18n-data.js` | Motor bilingüe EN/ES propio | ⏸️ No construido — sitio monolingüe por ahora. Se agrega si el cliente confirma bilingüe. |
| `footer-map.js` | Popover de mapa Leaflet | ✅ No aplica — sin mapa. |
| `README.md` | Descripción del proyecto JPO | Este mismo archivo — brief vivo, actualizado en cada sesión de trabajo. |

> **Nota v2:** `css/style.css` (reset + tipografía base) volvió a activarse en `<link>` de `index.html` — en v1 quedó huérfano tras la modularización. `css/tokens.css`, `css/layout.css`, `css/header.css`, `css/components.css` y `js/main.js` fueron reescritos para el sistema glassmorphism (ver §1-bis). `favicon.svg` se actualizó a la nueva paleta.

---

## 5. Checklist de pendientes reales

- [x] Especialidad exacta confirmada — tecnología e ingeniería de la construcción
- [x] Ubicación confirmada (país) — Canadá
- [x] Paleta/identidad visual confirmada — ink/paper/bronze, construida en `css/tokens.css`
- [x] Decisión sobre chatbot — no lleva
- [x] Decisión sobre mapa — no lleva por ahora
- [x] Idioma(s) del sitio confirmado — monolingüe ES
- [ ] Nombre del negocio definitivo (hoy: "ETEXCA" temporal)
- [ ] Ciudad específica dentro de Canadá
- [ ] Lista de servicios confirmada por el cliente (hoy: placeholder razonado de 5 servicios típicos del rubro)
- [ ] Correo corporativo (sin dominio propio aún) y teléfono
- [ ] Backend/destino real del formulario de contacto (depende del correo corporativo)
- [ ] Carpeta de imágenes: nombres/rutas confirmados

---

## 6. Estado actual
🟢 **Fase de construcción activa.** `index.html`, los 4 archivos de `css/` y `js/main.js` están escritos y funcionales, con copy real donde había datos (nombre temporal, especialidad, servicios, país) y placeholders explícitos donde no (correo, teléfono, ciudad exacta). El sitio es navegable y responsive tal como está. Lo que sigue depende del cliente: nombre definitivo, correo corporativo, y confirmación/ajuste de la lista de servicios — no hay más decisiones de arquitectura pendientes de nuestro lado.
