# Assets corporativos — Claro/VTR

Iconos extraídos del template oficial PowerPoint Claro 2026, listos para usar en la guía comercial.

## Cómo usarlos

### Paso 1 — Subir al repositorio GitHub

Sube esta carpeta `assets/` completa al mismo directorio donde está `guia_comercial_express.html` en tu repo de GitHub.

Estructura esperada:

```
tu-repo/
├── guia_comercial_express.html
└── assets/
    ├── logo-claro.svg
    ├── logo-claro-watermark.png
    ├── icon-bag.png
    ├── icon-bolt.png
    ├── icon-bulb.png
    ├── icon-cycle-heart.png
    ├── icon-flag.png
    ├── icon-handshake.png
    ├── icon-heart-spark.png
    ├── icon-person.png
    ├── icon-play-triangle.png
    ├── icon-puzzle.png
    ├── icon-star-burst.png
    ├── icon-wifi.png
    ├── icon-arrow-curve.png
    └── icon-arrow-down.png
```

### Paso 2 — Insertar un ícono en el HTML

El CSS ya está incluido en la guía (clase `.icon-corp`). Solo agregas el `<span>` donde lo necesites:

```html
<!-- Tamaño chico (18×18) - inline con texto -->
<span class="icon-corp size-sm"><img src="assets/icon-wifi.png" alt=""></span>

<!-- Tamaño medio (28×28) - títulos, badges -->
<span class="icon-corp size-md"><img src="assets/icon-star-burst.png" alt=""></span>

<!-- Tamaño grande (48×48) - cards, secciones -->
<span class="icon-corp size-lg"><img src="assets/icon-handshake.png" alt=""></span>

<!-- Extra grande (72×72) - hero sections -->
<span class="icon-corp size-xl"><img src="assets/icon-flag.png" alt=""></span>
```

## Catálogo de íconos disponibles

| Archivo | Sugerencia de uso |
|---|---|
| `icon-bag.png` | Compras, ofertas, planes |
| `icon-bolt.png` | Velocidad, nuevas tácticas, flash |
| `icon-bulb.png` | Tips, ideas, recomendaciones |
| `icon-cycle-heart.png` | Renovación, fidelización, retención |
| `icon-flag.png` | Verticales, proyectos, hitos |
| `icon-handshake.png` | Dealers, acuerdos comerciales, partnerships |
| `icon-heart-spark.png` | Experiencia cliente, satisfacción |
| `icon-person.png` | Línea adicional, ejecutivos, clientes |
| `icon-play-triangle.png` | Inicio, comenzar, continuar |
| `icon-puzzle.png` | Integración, soluciones, packs |
| `icon-star-burst.png` | Precios estrella, destacados |
| `icon-wifi.png` | Internet, fibra, conectividad |
| `icon-arrow-curve.png` | Cambio, migración, redirección |
| `icon-arrow-down.png` | Descargar, profundizar, descenso |
| `logo-claro.svg` | Logo oficial Claro vectorial (rojo) |
| `logo-claro-watermark.png` | Logo Claro tono claro para fondos oscuros |

## Ejemplos prácticos donde aplicarlos

### Ejemplo 1 — Reemplazar el ⭐ por icon-star-burst en "Precios Estrella"

**Antes:**
```html
<div class="section-label red">⭐ Precios Estrella del Mes</div>
```

**Después:**
```html
<div class="section-label red">
  <span class="icon-corp size-sm" style="margin-right:5px">
    <img src="assets/icon-star-burst.png" alt="">
  </span>
  Precios Estrella del Mes
</div>
```

### Ejemplo 2 — Header oficial con logo grande en login

**Antes:** logo CLAROVTR de texto pequeño

**Después:** SVG oficial Claro (ya implementado en v5)

### Ejemplo 3 — Card destacada con ícono corporativo

```html
<div class="offer-card">
  <div style="display:flex;align-items:center;gap:10px;margin-bottom:8px">
    <span class="icon-corp size-lg">
      <img src="assets/icon-bolt.png" alt="">
    </span>
    <div>
      <div class="offer-name">Nueva Táctica L</div>
      <div style="font-size:10px;color:#9CA3AF">Velocidad y mejor precio</div>
    </div>
  </div>
  <!-- resto de la card -->
</div>
```

## Tip para WhatsApp / impresión

Si vas a compartir la guía por WhatsApp o necesitas imprimirla, prefiere mantener el HTML autocontenido (con SVG inline). En ese caso, los iconos que más uses los puedes convertir a base64 con esta herramienta online:

https://www.base64-image.de/

Y luego usarlos así (sin necesidad de archivo externo):

```html
<span class="icon-corp size-md">
  <img src="data:image/png;base64,iVBORw0KGgo..." alt="">
</span>
```

---

**Nota:** todos los íconos están extraídos del template oficial Claro 2026 y son de uso interno autorizado.
