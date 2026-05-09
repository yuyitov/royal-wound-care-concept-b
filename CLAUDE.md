# Royal Wound Care — Maqueta Estática (Concepto) — VERSIÓN B

⚠️ Este es el directorio de la **VERSIÓN B**. Nunca modificar el directorio de la Versión A.
- **Versión A** (congelada): https://yuyitov.github.io/royal-wound-care-concept/
- **Versión B** (activa): https://yuyitov.github.io/royal-wound-care-concept-b/
- **Repo B**: https://github.com/yuyitov/royal-wound-care-concept-b
- **Directorio local B**: `C:\Users\veron\Documents\royal-wound-care-concept-b`

Este proyecto es una maqueta externa segura y estática para Royal Wound Care.
No es el sitio real. No está conectado a ningún sistema de producción.

---

## Reglas de trabajo

- No tocar el sitio real en GoHighLevel ni el dominio real.
- No conectar formularios reales ni capturar datos de pacientes.
- No incluir PHI ni información sensible.
- No agregar tracking, analytics, backend, base de datos, npm, React ni scripts externos.
- **Excepción aprobada**: Google Fonts (Playfair Display + Lato) son las fuentes oficiales de la marca.
- Cada página es un archivo HTML estático con CSS interno y JavaScript mínimo.
- Siempre leer el HTML actual antes de proponer cambios.
- No modificar archivos hasta que el usuario apruebe el checklist.
- **Nunca usar PowerShell `Set-Content` o `Get-Content` para editar HTML** — corrompe caracteres UTF-8. Usar siempre la herramienta Edit o Python para reemplazos masivos.

## Proceso para cambios

1. Leer el archivo HTML actual de la sección relevante.
2. Proponer checklist de cambios al usuario.
3. Aplicar solo tras aprobación explícita.
4. Hacer commit y push después de cada cambio aprobado.

---

## Archivos del proyecto

| Archivo | Descripción |
|---|---|
| `index.html` | Página principal (Home) |
| `skilled-nursing-facilities.html` | Subpágina de Skilled Nursing Facilities |
| `wound-vac-support.html` | Subpágina de Wound VAC Support |

---

## Identidad Visual Oficial

Fuente: export JSON de GoHighLevel — `royalwoundcare.com_.2026-04-23.json`

### Paleta de colores (`:root` en todos los archivos)

```css
--navy:        #1F3B68;   /* Color principal — texto, fondos oscuros, botones primarios */
--navy-mid:    #2A4F85;
--navy-light:  #3566A0;
--navy-dark:   #132845;   /* Fondo más oscuro — sección carrusel de servicios */
--royal-blue:  #0B6FAE;
--medical-blue:#1769C2;
--teal:        #2CA6A4;   /* Acento principal — borde left en about-points, top del CTA */
--teal-dark:   #228582;   /* Labels de sección, text-links */
--teal-light:  #5BBFBD;   /* Números en carrusel, detalles secundarios */
--gold:        #F2C57C;   /* Secundario — botones gold, hero cards, header-action-btn */
--gold-light:  #F8DBA5;
--gold-dark:   #D4A552;
--white:       #FFFFFF;
--soft-bg:     #F4F8F8;   /* Fondo de secciones alternadas */
--ink:         #1F3B68;   /* Alias de --navy para texto */
--muted:       #6B7B8D;   /* Texto secundario / descripciones */
--line:        #E4EDED;   /* Bordes de tarjetas y divisores */
--shadow:      0 22px 70px rgba(31, 59, 104, 0.14);
--radius-xl:   28px;
--radius-lg:   22px;
--radius-md:   16px;
```

### Tipografía

- **Headings**: `'Playfair Display'` — weights 600, 700, italic 600. Serif elegante.
- **Body / Nav / Botones**: `'Lato'` — weights 400, 700, 900.
- **Fallbacks heading**: `Georgia, "Times New Roman", serif`
- **Fallbacks body**: `ui-sans-serif, system-ui, Arial, sans-serif`
- **Google Fonts URL**:
  ```
  https://fonts.googleapis.com/css2?family=Lato:wght@400;700;900&family=Playfair+Display:ital,wght@0,600;0,700;1,600&display=swap
  ```

**Tamaños usados:**
- H1 hero: `clamp(52px, 5.5vw, 80px)`
- H2 secciones: `clamp(34px, 4vw, 58px)`
- Body: `15–17px`, line-height `1.55–1.65`
- Labels uppercase: `13px`, `font-weight: 900`, `letter-spacing: .12em`
- Nav links: `16px`, Georgia (no Playfair), `font-weight: 700`

### Cursor personalizado (todas las páginas)

Cursor de curita animada en SVG — aplicado en `html` y `body`:
```css
cursor: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='32' height='32' viewBox='0 0 32 32'%3E%3Cg transform='rotate(-28 16 16)'%3E%3Crect x='5' y='11' width='22' height='10' rx='5' fill='%23F2C57C' stroke='%231F3B68' stroke-width='1.2'/%3E%3Crect x='12' y='11' width='8' height='10' fill='%23FFE4B3' opacity='0.95'/%3E%3Ccircle cx='14' cy='14' r='1' fill='%232CA6A4'/%3E%3Ccircle cx='18' cy='14' r='1' fill='%232CA6A4'/%3E%3Ccircle cx='14' cy='18' r='1' fill='%232CA6A4'/%3E%3Ccircle cx='18' cy='18' r='1' fill='%232CA6A4'/%3E%3C/g%3E%3C/svg%3E") 6 6, auto;
```

---

## Layout del Header (index.html)

El header usa `display: grid` con 2 columnas y 2 filas en `.topbar`:

```
[ LOGO (col1, row1-2) ] [ header-actions: Book Now | Blog  (col2, row1) ]
                         [ nav-list: About | Services▼ | Partner▼ | ... (col2, row2) ]
```

- `.topbar`: `position: sticky; top: 0; z-index: 100; backdrop-filter: blur(18px)`
- `.site-header`: `display: contents` — los hijos se colocan en el grid del topbar
- Logo: `width: 214px`, padding izquierdo `32px`
- Header actions: fondo `var(--gold)`, color `var(--navy)`, `border-radius: 8px`, sombra gold
- Blog button: fondo `var(--navy)`, texto blanco
- Nav alineado a la derecha (`justify-content: flex-end`)

### Dropdown nav

- Aparece en hover con `opacity` transition, `top: 100%`, centrado con `translateX(-50%)`
- `border-radius: 16px`, `box-shadow: 0 18px 48px rgba(31,59,104,.16)`
- Links en Georgia 14px, color `#1a3558`, hover fondo `#f4f7fb`
- Las flechas de dropdown usan entidad HTML `&#8250;` (›), chevrons `&#9660;` (▼)

### Items del nav (con submenús definidos)

- **About Us** → `#why-royal`
- **Our Services** ▼ → Skilled Nursing Facilities | Wound VAC Support | Mobile Wound Care | In-Clinic | Home Health | SNF Partners
- **Become a Partner** ▼ → What Our Partners Experience
- **Wound Care** ▼ (dropdown wide) → Why wound care | Advanced Wound Treatments | + 7 temas
- **Resources** ▼ → Board-Certified | Blog | Contact | FAQ
- **Education** ▼ → Wound Care Nurse Certification | Nursing Education Credits | Medical Education Credits | Wound Care Course (Coming soon — disabled)

---

## Botones

Todos los botones: `border-radius: 8px`, con sombra de profundidad.

| Clase | Fondo | Texto | Sombra |
|---|---|---|---|
| `.btn-primary` | `var(--navy)` | `var(--white)` | `0 8px 24px rgba(31,59,104,.32)` |
| `.btn-teal` | `var(--gold)` | `var(--navy)` | `0 8px 24px rgba(242,197,124,.36)` |
| `.btn-interest` | `var(--gold)` | `var(--navy)` | `0 12px 32px rgba(242,197,124,.38)` — más grande (66px alto) |
| `.header-action-btn` | `var(--gold)` | `var(--navy)` | `0 8px 20px rgba(242,197,124,.36)` |

**Nota importante**: Los botones dorados tienen texto en `var(--navy)` — NO blanco (contraste aprobado por la usuaria).

---

## Secciones del Home (orden)

1. **Hero** (`#home`) — navy gradient con parallax, 2 hero cards doradas animadas
2. **Wound VAC / New Service** (`#wound-drainage`) — sección con 2 columnas, fondo blanco
3. **Education** (`#wound-care-course`) — 4 items: Nurse Certification, Nursing Credits, Medical Credits, Wound Care Course (Coming soon)
4. **Patients / Audience** (`#patients`) — 4 audience cards con mini-icons
5. **Why Royal Wound Care** (`#why-royal`) — about-card navy + 4 about-points con `border-left: 3px solid var(--teal)`
6. **Specialized Services** (`#services`) — CARRUSEL INFINITO, fondo dark navy, 18 tarjetas glass
7. **Partners** (`#partners`) — 6 logos reales en grid 3×2
8. **Royal Wound Care Blog** (`#resources`) — 3 artículos reales del blog
9. **CTA Final** (`#appointment`) — panel con `border-top: 3px solid var(--teal)`
10. **Footer** (`#contact`) — 2 ubicaciones reales

---

## Hero (index.html)

- Fondo: `background: var(--navy)` con parallax JS y orbs en pseudo-elementos
- Orb teal izquierdo: `rgba(44,166,164,.34)` — grande, fuera de pantalla izq.
- Orb gold derecho: `rgba(242,197,124,.10)` — sutil
- Orb teal adicional bottom-right: `rgba(44,166,164,.16)`
- Altura: `min-height: clamp(360px, calc(100vh - 90px), 380px)`
- 2 hero-choice-cards doradas con animaciones de entrada + glow pulsante

### Hero cards doradas

```css
background: linear-gradient(145deg, var(--gold-light) 0%, var(--gold) 42%, var(--gold-dark) 100%);
color: var(--navy);
animation: heroCardIn .85s cubic-bezier(.22,1,.36,1) both, cardGlow 3.2s ease-in-out infinite;
```
- Card 1 delay: `.28s, 1.2s`
- Card 2 delay: `.52s, 1.5s`

---

## Carrusel de Servicios Especializados

- **Fondo sección**: degradado dark con glow teal y gold:
  ```css
  radial-gradient(ellipse at 75% 55%, rgba(44,166,164,.13), transparent 52%),
  radial-gradient(ellipse at 10% 20%, rgba(242,197,124,.07), transparent 40%),
  linear-gradient(148deg, #061728 0%, #0D2240 38%, #122d50 68%, #0A1C38 100%)
  ```
- **Intro 2 columnas**: h2 izquierda (38px), descripción + 3 stats derecha
- **18 tarjetas** duplicadas a 36 para loop infinito (CSS `@keyframes carouselScroll`)
- Velocidad: `animation: carouselScroll 65s linear infinite`
- Se pausa en hover: `animation-play-state: paused`
- Fade lateral: `mask-image: linear-gradient(to right, transparent 0%, black 6%, black 94%, transparent 100%)`

### Tarjetas glass (estado normal — en movimiento)

```css
flex: 0 0 310px;
min-height: 220px;
background: linear-gradient(160deg, rgba(255,255,255,.13) 0%, rgba(255,255,255,.05) 100%);
border: 1px solid rgba(255,255,255,.18);
backdrop-filter: blur(20px);
box-shadow: 0 4px 28px rgba(0,0,0,.32), inset 0 1px 0 rgba(255,255,255,.28);
```
- `::after`: white radial glow arriba (siempre visible)
- `::before`: línea teal 2px (solo en hover)

### Tarjetas glass (estado hover)

```css
background: linear-gradient(160deg, rgba(44,166,164,.18) 0%, rgba(44,166,164,.07) 100%);
border-color: rgba(44,166,164,.40);
box-shadow: 0 8px 36px rgba(44,166,164,.20), inset 0 1px 0 rgba(255,255,255,.30);
```

### Tipografía dentro de tarjetas

- Número: `10px`, `color: var(--teal-light)`, `opacity: .8`
- Título (h3): `Playfair Display`, `19px`, blanco
- Descripción (p): `15px`, `rgba(255,255,255,.88)` — casi blanco puro

---

## Partners Section

- 6 logos reales en grid `repeat(3, 1fr)`, gap `16px`
- Cards: `border-radius: 22px`, hover con `border-color: rgba(44,166,164,.35)` y sombra teal
- Logo URL base: `https://images.leadconnectorhq.com/image/f_webp/q_80/r_1200/u_https://assets.cdn.filesafe.space/FtBJCK1GLpMIqS57PbDJ/media/`

| Partner | Archivo |
|---|---|
| Active Plus Home Health | `67e6f01d13c4b647cd0fd0bb.png` |
| Ameri Hospice Care | `67e6f01799a78ccd07a17f94.png` |
| Chatsworth Park Health Care Center | `67e6f014b60b7756e75ba0a4.jpeg` |
| VITAS Palliative Care | `67e6f010f523c7da221685a5.png` |
| Tri-Valley Hospice Care | `67e6f00d379294e789e44c61.png` |
| Option One Home Care Inc. | `67e6f008c5f22a26c4aad7b5.png` |

---

## Logo oficial

```
https://images.leadconnectorhq.com/image/f_webp/q_80/r_1200/u_https://assets.cdn.filesafe.space/FtBJCK1GLpMIqS57PbDJ/media/67e3d2bf2be3f75e0f215e50.png
```

---

## Footer (datos reales)

```html
<strong>West Hills</strong>
7230 Medical Center Dr. Suite 100, West Hills, CA 91307
Tel: (818) 660-2977

<strong>Beverly Hills</strong>
9735 Wilshire Blvd #210B, Beverly Hills, CA 90212
Tel: (818) 660-2977
```

---

## Acentos teal aplicados en el diseño

- `about-point`: `border-left: 3px solid var(--teal)`
- `.final-cta .panel`: `border-top: 3px solid var(--teal)` + `box-shadow` con glow teal
- Partner cards hover: `border-color: rgba(44,166,164,.35)`
- Hero: orb teal reforzado `.34` opacidad + glow adicional bottom-right

---

## Subpáginas creadas

### skilled-nursing-facilities.html
- Header idéntico al home pero con clase `.topbar` y CSS prefijado
- Nav links apuntan a `index.html#anchor`
- Tiene sección de 18 clinical services, proceso de partnership, beneficios, métricas

### wound-vac-support.html
- Página de Wound VAC Support con copy placeholder
- Secciones: Hero, What is Wound VAC, Supply Model (fondo dark navy), How it Works, Who Benefits (6 cards), FAQ (acordeón `<details>`), CTA
- Enlazada desde home: botón "View More" en sección New Service + dropdown nav "Our Services"
- CTA del home: 2 botones — "Join the Interest List" (abre modal) + "View More" → wound-vac-support.html

---

## Decisiones de diseño confirmadas por la usuaria

- Botones: radio `8px` (no 0px ni 50px del export original) — aprobado
- Botones dorados: texto navy (no blanco) — mejor contraste — aprobado
- Hero cards: doradas (no glassmorphism) — aprobado
- Carrusel: blanco-glass en movimiento, teal al hover — aprobado (no al revés)
- Blog: artículos reales de royalwoundcare.com — aprobado
- Google Fonts: excepción a "no scripts externos" por ser fuentes oficiales de marca — aprobado
- Labels de sección (`Specialized Services`, etc.): solo texto teal, SIN fondo pill — aprobado (se probó y se revirtió)
