# Prompt: optimización y simplificación del sitio Kadol

> Prompt reutilizable para pedir (a Claude u otro desarrollador) la reestructuración del sitio kadoluniformes.cl.
> Este archivo empieza con `_` para que GitHub Pages no lo publique.

---

Actúa como desarrollador front-end y diseñador web senior. Vas a simplificar y optimizar el sitio estático de **Kadol SpA** (vestuario corporativo, industrial, calzado y EPP para empresas en Chile; dominio `kadoluniformes.cl`). El sitio es HTML/CSS/JS puro, sin framework ni build.

## Objetivo
Pasar de un catálogo con carro y selección de productos a un sitio de **generación de contactos**: el usuario entiende qué hace Kadol, ve a quién le ha vendido, identifica la familia de productos que necesita y deja sus datos. **El único CTA es "Contactar".**

## Estructura final (3 páginas)

### 1. `index.html` (Home), en este orden
1. **Hero con propuesta de valor.** Titular corto ("Vestimos y protegemos a tu equipo"), bajada que explique que Kadol asesora, compara proveedores y entrega una propuesta a medida. CTA principal "Contactar" → `contacto.html`, CTA secundario "Ver productos" → `#familias`. Tres datos de respaldo: 30+ años de experiencia, n.º de clientes, n.º de marcas.
2. **Logos de clientes** (`assets/logos-clientes/`), en carrusel continuo en escala de grises.
3. **Familias de productos** con el encabezado exacto:
   - Título: **"¿Qué necesita tu equipo?"**
   - Bajada: **"Déjanos tu contacto y te ayudamos a encontrar lo que buscas."**
   - Tarjetas con imagen + nombre + descripción + enlace "Cotizar" que lleve a `contacto.html?familia=<slug>` y precargue el mensaje del formulario.
   - Familias y descripciones (textos del cliente, pendientes de revisión final de Andrés):
     | Familia | Descripción |
     |---|---|
     | Vestuario Corporativo | Una imagen profesional para todo tu equipo. |
     | Vestuario Corporativo Universidades e Institutos Profesionales | Comodidad e identidad institucional para tu equipo. |
     | Vestuario Corporativo Colegios | Vestuario, prendas y delantales para quienes educan, con la identidad de cada colegio. |
     | Vestuario Industrial | Prendas para el trabajo diario en terreno y planta. |
     | Vestuario Vial | Vestuario de alta visibilidad para trabajos en ruta. |
     | Vestuario para Minería | Vestuario y accesorios para tu equipo en faena. |
     | Calzado | Calzado para cada función de tu equipo. |
     | Protección Personal · EPP | Equipos de protección personal certificados y de alta calidad para cabeza, ojos, audición, respiración, manos, pies, trabajo en altura y frío/calor. |
     | Guardias de Seguridad | Uniformes para equipos de vigilancia y seguridad. |
     | Conserjería y Recepción | Una presentación profesional para quienes reciben y atienden. |
     | Personal de Cocina | Viste a tu equipo para cada jornada en cocina. |
     | Personal Médico | Delantales y vestuario clínico para profesionales de la salud. |
     | TENS y Personal de Salud | Conjuntos clínicos para quienes cuidan a los demás. |
   - Imágenes del cliente: calzado (panorámica de 5 zapatos), Universidades (polera y polar UDLA), Colegios (polera y delantal Colegio La Abadía), EPP (casco, fonos, chaleco, arnés, etc.).
4. **Cómo trabajamos** (reemplaza la sección antigua "Selección / Comparación / Confirmación"):
   - **01 / Contacto:** Nos entregas tus antecedentes y nos comunicamos con tu empresa.
   - **02 / Solicitud:** Revisamos tu solicitud y buscamos alternativas de distintos proveedores según calidad, precio y volumen.
   - **03 / Confirmación:** El precio, la disponibilidad, los antecedentes técnicos y el plazo se validan antes de confirmar el pedido.
5. **Marcas con las que trabajamos** (`assets/img/logos-marcas/`), en grilla de logos.
6. **Cierre:** banda de color con "Cuéntanos qué necesita tu equipo" + botón "Contactar" y botón secundario de WhatsApp.

### 2. `contacto.html`
- Formulario corto: **Nombre, Teléfono, Correo** (obligatorios) y **Mensaje** (opcional).
- Debe **enviar de verdad** (el formulario actual no envía nada). Sin backend propio, se usa FormSubmit (`https://formsubmit.co/ajax/contacto@kadol.cl`) con honeypot antispam, estado de éxito o error visible y alternativa por WhatsApp/correo si falla.
- Lee `?familia=` de la URL y precarga "Me interesa cotizar: <familia>".
- Columna lateral con WhatsApp, correo y los 3 pasos del proceso.

### 3. `nosotros.html`
- Historia (fundada en 2019 por Andrés Carvajal y Jorge Olea, 30 años de experiencia), 3 datos de valor, galería de trabajos realizados con visor (lightbox) y cierre con CTA.

## Eliminar
- `productos.html` (catálogo, carro y selección de productos) y `cotizacion.html`. Dejarlas como redirección a `index.html#familias` y `contacto.html` para no romper enlaces antiguos.
- Tailwind por CDN (`cdn.tailwindcss.com`): reemplazar por un único CSS propio (`assets/css/site.css`).

## Requisitos técnicos
- **Rendimiento:** todas las imágenes en WebP, a un máximo de ~1400 px de ancho, con `loading="lazy"` fuera del hero; nada de PNG de 13 MB ni archivos `.heic`.
- **SEO:** `title` y `meta description` únicos por página, Open Graph, `canonical`, favicon, `robots.txt`, `sitemap.xml` y JSON-LD `Organization`.
- **Accesibilidad:** textos alternativos descriptivos, foco visible, `aria-current` en el menú, carrusel detenido si `prefers-reduced-motion`, lightbox cerrable con Escape.
- **Responsive:** funciona desde 360 px sin scroll horizontal.
- **Contenido:** español de Chile con tildes correctas y un solo correo (`contacto@kadol.cl`).
- **Identidad visual (estilo catálogo B2B impreso, evitar look genérico de plantilla):** fondo papel `#f2f0eb`, tinta `#17202a`, naranjo de seguridad `#d4521c` solo como acento. Una sola tipografía, Archivo (con eje de ancho para cifras y logotipo). Títulos en minúscula normal, nunca todo en mayúsculas. Estructura con reglas finas y un índice numerado por sección. Esquinas rectas, sin sombras, degradados, tarjetas flotantes, carruseles ni etiquetas en mayúsculas espaciadas.

## Pendientes a confirmar con el cliente
- Revisión de descripciones por Andrés.
- Fotos para **Personal de Cocina**, **TENS y Personal de Salud** y una foto real de **Guardias de Seguridad**.
- Activar FormSubmit: el primer envío llega a contacto@kadol.cl con un enlace de confirmación.
- Logo oficial de Kadol (hoy es una "K" provisional).
