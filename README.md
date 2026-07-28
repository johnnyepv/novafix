# NovaFix — Landing Page

Sitio web de una sola página para **NovaFix**, empresa de soporte técnico e infraestructura IT con sede en Buenaventura, Colombia. Presenta el portafolio de servicios, información de contacto y un formulario de solicitud de cotización.

🔗 **Sitio en producción:** www.novafix.com *(pendiente de confirmar dominio activo)*

---

## Contenido

- [Stack técnico](#stack-técnico)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Ver el sitio en local](#ver-el-sitio-en-local)
- [Despliegue (GitHub + Netlify)](#despliegue-github--netlify)
- [Formulario de contacto (Netlify Forms)](#formulario-de-contacto-netlify-forms)
- [SEO y datos estructurados](#seo-y-datos-estructurados)
- [Pendientes conocidos](#pendientes-conocidos)
- [Contacto](#contacto)

---

## Stack técnico

- **HTML5** + **Bootstrap 5.3** (CDN, con integridad SRI habilitada)
- **CSS** personalizado (variables de marca, animaciones de entrada con `IntersectionObserver`)
- **JavaScript vanilla** — sin frameworks ni dependencias de build
- **Netlify Forms** para el manejo del formulario de contacto (sin backend propio)
- **Schema.org (JSON-LD)** para SEO local tipo `LocalBusiness`
- Hosting: **GitHub** (repositorio) + **Netlify** (build y despliegue continuo)

No requiere `npm install` ni proceso de build — es un sitio estático puro.

---

## Estructura del proyecto

```
/
├── index.html          # Página principal (única página del sitio)
├── img/
│   ├── logo-novafix.png
│   ├── favico.png
│   └── backgrounddiv.png
└── README.md
```

> **Nota:** confirma que las 3 imágenes referenciadas en `img/` existan en el repositorio antes de desplegar — si faltan, el logo, el ícono de pestaña o el fondo de la sección de servicios no se verán.

---

## Ver el sitio en local

No necesita servidor especial. Basta con:

1. Clonar el repositorio.
2. Abrir `index.html` directamente en el navegador, **o** servirlo con un servidor local simple para evitar problemas de rutas relativas:
   ```bash
   npx serve .
   ```
   o
   ```bash
   python3 -m http.server 8000
   ```

⚠️ El formulario de contacto **no funcionará en local** — Netlify Forms solo procesa envíos en sitios desplegados en Netlify.

---

## Despliegue (GitHub + Netlify)

1. Sube el contenido de este repositorio a GitHub (rama `main`).
2. En [Netlify](https://app.netlify.com) → **Add new site → Import an existing project → GitHub** → selecciona el repositorio.
3. Configuración de build:
   - **Build command:** *(vacío, no aplica — sitio estático)*
   - **Publish directory:** `.` (raíz del repo, donde está `index.html`)
4. Deploy.
5. Verifica en **Site configuration → Forms** que Netlify detectó el formulario `contacto-novafix` después del primer deploy (puede requerir activar manualmente **"Form detection"** en Forms → Settings si no aparece).

Cada `git push` a `main` dispara un nuevo deploy automático.

---

## Formulario de contacto (Netlify Forms)

El formulario (`id="form-contacto"`, `name="contacto-novafix"`) usa detección nativa de Netlify:

- `data-netlify="true"` en el `<form>` — necesario para que Netlify lo detecte en el HTML publicado.
- Campo honeypot oculto `bot-field` — filtro anti-spam invisible para personas.
- Envío por **AJAX** (`fetch`) — evita recargar la página y muestra un mensaje de confirmación in-line (`#form-success` / `#form-error`).

### Notificaciones

Configuradas en **Netlify → Forms → Settings and usage → Form notifications**, con una notificación de tipo *Email* apuntando a `contacto.novafix@gmail.com`.

**Si las notificaciones no llegan al correo:**
- Revisar la carpeta de Spam en Gmail (los correos llegan desde `formresponses@netlify.com`).
- Confirmar en la pestaña **Forms** de Netlify que los envíos de prueba no estén cayendo en la sección de **Spam** del propio Netlify (puede pasar si el campo honeypot llega mal vacío).
- Como alternativa gratuita si las notificaciones por correo dan problemas: configurar una notificación de tipo **Outgoing webhook** apuntando a un flujo de [Pipedream](https://pipedream.com) o Zapier (plan gratuito) que reenvíe el correo.
- Alternativa completa si se decide dejar Netlify Forms: [Web3Forms](https://web3forms.com) (250 envíos/mes gratis, notificación por correo incluida) o [Formspree](https://formspree.io) (50 envíos/mes gratis).

---

## SEO y datos estructurados

- `<meta name="description">` y etiquetas **Open Graph** (`og:title`, `og:description`, `og:image`, `og:url`) para que el sitio se vea bien al compartirse en redes/WhatsApp.
- Bloque **JSON-LD `LocalBusiness`** en el `<head>` con nombre, teléfono, dirección y descripción — debe mantenerse sincronizado con los datos del perfil de **Google Business Profile** una vez se cree.
- Snippet de **Google Analytics 4** dejado comentado en el `<head>`, listo para activar reemplazando `G-XXXXXXXXXX` por el ID real una vez se genere en [analytics.google.com](https://analytics.google.com).

Para que el sitio aparezca en resultados de búsqueda de Google:
1. Verificar el dominio en [Google Search Console](https://search.google.com/search-console) y enviar el sitemap.
2. Crear y verificar el [Google Business Profile](https://business.google.com) de NovaFix con los mismos datos del sitio (nombre, dirección, teléfono).

---

## Pendientes conocidos

- [ ] Confirmar que el dominio `novafix.com` esté comprado y apuntando al sitio en Netlify.
- [ ] Reemplazar los testimonios de ejemplo en la sección "Lo que dicen nuestros clientes" por reseñas reales.
- [ ] Reemplazar `og:image` por una imagen de portada real subida al repositorio (actualmente apunta a una URL de ejemplo).
- [ ] Comprimir/convertir `logo-novafix.png` y `backgrounddiv.png` a WebP para mejorar el rendimiento.
- [ ] Activar Google Analytics 4 con un ID real.
- [ ] Verificar entrega de notificaciones por correo del formulario de contacto (ver sección anterior).
- [ ] Revisar el texto de los modales de Aviso Legal y Política de Privacidad con un abogado antes de publicarlos formalmente.

---

## Contacto

- **WhatsApp / Teléfono:** +57 317 803 0414
- **Correo:** contacto.novafix@gmail.com
- **Dirección:** Cr 19 Cl 4 - 30, Buenaventura, Colombia
