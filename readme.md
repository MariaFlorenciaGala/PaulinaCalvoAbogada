# Landing para Abogada de Familia Online

Landing page de una sola página para captar consultas online de una **abogada de familia en Córdoba, Argentina**. Está pensada para tráfico pago (Google Ads y Meta Ads): un único objetivo (que la persona escriba por WhatsApp), carga rápida y un mensaje que se adapta al anuncio que la trajo.

<p align="center">
  <img src="assets/preview.jpg" alt="Vista previa de la landing" width="720">
</p>

<p align="center">
  <img alt="HTML5" src="https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white">
  <img alt="CSS3" src="https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white">
  <img alt="JavaScript" src="https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black">
  <img alt="Sin dependencias" src="https://img.shields.io/badge/dependencias-0-success">
  <img alt="Deploy en Netlify" src="https://img.shields.io/badge/deploy-Netlify-00C7B7?logo=netlify&logoColor=white">
</p>

---

## Características

- **Conversión por WhatsApp:** botones, tarjetas, barra fija en móvil y botón flotante abren `wa.me` con un mensaje ya escrito según el tema.
- **Formulario corto:** nombre, tema y detalle opcional. Valida y abre WhatsApp con la consulta armada; no se guarda ningún dato en el sitio.
- **Mensaje alineado con el anuncio:** con `?tema=` en la URL cambian el titular, el subtítulo y el título de la pestaña, se preselecciona el formulario y se resalta el servicio correspondiente.
- **Atribución de campañas:** conserva `utm_*`, `gclid`, `gbraid`, `wbraid` y `fbclid`, y los envía en cada evento.
- **Tracking listo para usar:** Google Ads, Meta Pixel y `dataLayer` para Google Tag Manager, activos solo si se cargan los IDs.
- **Rápida:** sin frameworks ni build, íconos SVG en línea, imágenes WebP con medidas fijas y carga diferida.
- **SEO local:** datos estructurados JSON-LD (`Attorney`), Open Graph y metadatos.
- **Accesible y responsive:** formularios con etiquetas, atributos `aria` en el menú y las preguntas frecuentes, `prefers-reduced-motion` y diseño pensado primero para móvil.

**Secciones:** hero con formulario · barra de confianza · situaciones y servicios (incluye redacción de documentos) · por qué online · proceso en 4 pasos · banda de contacto · sobre mí · preguntas frecuentes · contacto · footer legal y política de privacidad.

## Estructura

```
abogadaOnline/
├── index.html      # Estructura, formularios, JSON-LD y JavaScript
├── styles.css      # Diseño: variables CSS, Grid, Flexbox y animaciones
├── _headers        # Netlify: caché de imágenes y encabezados de seguridad
├── readme.md
└── assets/
    ├── favicon.ico
    ├── favicon-192.png
    ├── logo.png                   # Apple touch icon y JSON-LD
    ├── preview.jpg                # Imagen para compartir (Open Graph, 1200×630)
    ├── paulina-retrato.webp
    ├── paulina-avatar.webp
    ├── paulina-videollamada.webp
    └── paulina-consulta.webp
```

## Inicio rápido

No requiere instalación ni build.

```bash
# Opción 1: abrir index.html en el navegador
# Opción 2: servidor local
npx serve .
```

**Publicación:** subir la carpeta a cualquier hosting estático. En Netlify alcanza con arrastrarla a *Sites → Add new site → Deploy manually*; el archivo `_headers` se aplica solo.

## Configuración

Todo lo editable está en el objeto `CONFIG`, al final de `index.html`:

| Clave | Descripción |
|---|---|
| `whatsapp` | Número en formato internacional, sin `+` ni espacios (54 + 9 + código de área + número) |
| `abogada` | Nombre completo; se replica en el logo, el footer y los mensajes |
| `nombreCorto` | Cómo se presenta en «Hola, soy…» |
| `email` | Correo de contacto |
| `gAdsId` | ID de Google Ads (`AW-XXXXXXXXXX`), opcional |
| `gAdsConversionLabel` | Etiqueta de la conversión de Google Ads, opcional |
| `metaPixelId` | ID del Meta Pixel, opcional |
| `refEnMensaje` | Agrega `(Ref: google/campaña)` al mensaje de WhatsApp cuando la visita viene de un anuncio |

Los textos de biografía, formación y horarios se editan directamente en el HTML; los que aún son provisorios aparecen resaltados en amarillo (clase `.todo`).

## Campañas de ads

### URLs finales por tema

| Grupo de anuncios | URL final |
|---|---|
| Divorcio | `https://tu-dominio.com/?tema=divorcio` |
| Cuota alimentaria | `https://tu-dominio.com/?tema=alimentos` |
| Cuidado de los hijos | `https://tu-dominio.com/?tema=cuidado` |
| Sucesiones | `https://tu-dominio.com/?tema=sucesion` |
| Unión convivencial | `https://tu-dominio.com/?tema=convivencia` |
| Convenios y homologación | `https://tu-dominio.com/?tema=acuerdos` |
| Redacción de documentos | `https://tu-dominio.com/?tema=documentos` |

Con parámetros de seguimiento:

```text
# Google Ads
https://tu-dominio.com/?tema=divorcio&utm_source=google&utm_medium=cpc&utm_campaign={campaignid}&utm_term={keyword}

# Meta Ads
https://tu-dominio.com/?tema=divorcio&utm_source=meta&utm_medium=paid&utm_campaign={{campaign.name}}
```

### Eventos

Se envían al `dataLayer` con la atribución adjunta:

| Evento | Cuándo se dispara |
|---|---|
| `landing_view` | Al cargar la página |
| `form_start` | Al empezar a completar un formulario |
| `scroll_50` / `scroll_90` | Al recorrer el 50 % y el 90 % de la página |
| `faq_open` | Al abrir una pregunta frecuente |
| `lead_whatsapp` | Al contactar por WhatsApp (con `lead_source` y `lead_tema`) |

La conversión de Google Ads y el evento `Lead` de Meta se disparan únicamente con `lead_whatsapp`.

### Recomendaciones

- En Google Ads, configurar la conversión con recuento **«Uno»** para que cada consulta cuente una sola vez.
- Activar el **etiquetado automático** y probar la URL final antes de lanzar.
- Evitar promesas de resultado en los textos del anuncio, tanto por la política de Google como por las normas de publicidad del Colegio de Abogados.

## Antes de publicar

- [ ] Reemplazar `TU-DOMINIO.com` en el canonical, Open Graph y JSON-LD.
- [ ] Cargar los IDs de seguimiento en `CONFIG`.
- [ ] Completar biografía, formación y horarios de atención.
- [ ] Confirmar con la titular las promesas del sitio: respuesta en el día hábil, presupuesto por escrito y alcance en la provincia de Córdoba.
- [ ] Verificar los datos de matrícula del footer.

## Diseño

Estilo editorial cálido, distinto del azul marino y dorado habitual en estudios jurídicos.

| Variable | Color | Uso |
|---|---|---|
| `--ivory` | `#F7F1E8` | Fondo principal |
| `--paper` | `#FFFBF5` | Tarjetas |
| `--ink` | `#221B18` | Texto |
| `--wine` | `#7A2436` | Acento principal |
| `--clay` | `#C9744E` | Acento secundario |
| `--sage` | `#DCE2D0` | Detalles suaves |
| `--wa` | `#178A45` | WhatsApp |

**Tipografías:** [Fraunces](https://fonts.google.com/specimen/Fraunces) para títulos y [Figtree](https://fonts.google.com/specimen/Figtree) para texto, servidas desde Google Fonts.

## Notas

- **Testimonios:** se omitieron a propósito; no se inventan reseñas. Cuando haya opiniones reales, con consentimiento, se puede sumar una sección reutilizando el estilo `.card`.
- **Datos personales:** el sitio no guarda datos. La política de privacidad del footer explica el uso de cookies de medición y los derechos de la Ley 25.326.

## Créditos

Diseñado y desarrollado por [Maria Florencia Gala](https://mariaflorenciagala.netlify.app/projects).
# PaulinaCalvoAbogada
# PaulinaCalvoAbogada
