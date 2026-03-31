# Implementación de AMP Analytics — Midas CDP

## Descripción general

Para los sitios que sirven páginas en formato AMP, la recolección de eventos se realiza a través del componente `amp-analytics`, que envía los datos directamente al backend del CDP. Los eventos se almacenan en el esquema `amp_events` del destino de Midas.

> **Importante:** Dado que AMP no permite la ejecución de JavaScript arbitrario, esta integración opera exclusivamente en **cloud mode**: los eventos se envían desde el navegador del usuario al backend, sin procesamiento en el dispositivo. No se soportan destinos que requieran ejecución en el cliente.

---

## Requisitos previos

Antes de agregar el snippet a una página AMP necesitas tener a mano dos valores, que el equipo de Midas te proporcionará:

| Variable | Descripción |
|---|---|
| `WRITE_KEY` | Clave de escritura de la fuente AMP registrada en el dashboard |
| `DATA_PLANE_URL` | URL del data plane del CDP (ej. `https://ingest.m1das.media`) |

---

## Paso 1 — Incluir el script del componente

Agrega la siguiente línea **antes del cierre de la etiqueta `</head>`** de tu página AMP:

```html
<script async custom-element="amp-analytics"
  src="https://cdn.ampproject.org/v0/amp-analytics-0.1.js"></script>
```

---

## Paso 2 — Agregar el bloque de configuración

Agrega el siguiente bloque **dentro de tu etiqueta `<body>`**, reemplazando `WRITE_KEY`, `DATA_PLANE_URL` y el nombre de la página:

```html
<amp-analytics config="https://cdn.rudderlabs.com/amp/rudderstack.json">
  <script type="application/json">
    {
      "vars": {
        "writeKey": "WRITE_KEY",
        "dataPlaneUrl": "DATA_PLANE_URL",
        "pageName": "Nombre de la página"
      }
    }
  </script>
</amp-analytics>
```

Con esta configuración mínima, el componente enviará automáticamente un evento `page` cada vez que se cargue la página.

> Si omites el campo `pageName`, el evento se registrará con el nombre `Unknown Page`.

---

## Paso 3 — Propiedades que se recolectan automáticamente

Sin ninguna configuración adicional, cada evento incluye las siguientes propiedades:

| Propiedad | Descripción |
|---|---|
| `anonymousId` | Identificador único del cliente AMP (`amp-<id>`) |
| `context.locale` | Idioma del navegador (ej. `es-CO`) |
| `context.page.path` | Ruta de la URL (ej. `/noticias/articulo-1`) |
| `context.page.url` | URL completa de la página |
| `context.page.referrer` | URL de referencia |
| `context.page.title` | Título del documento HTML |
| `context.screen.width` | Ancho de pantalla en píxeles |
| `context.screen.height` | Alto de pantalla en píxeles |

---

## Paso 4 (opcional) — Enviar propiedades adicionales

Si necesitas enriquecer los eventos con metadatos propios del contenido (sección, autor, ID del artículo, etc.), usa el objeto `extraUrlParams`. Cada propiedad debe tener el prefijo `properties.`:

```html
<amp-analytics config="https://cdn.rudderlabs.com/amp/rudderstack.json">
  <script type="application/json">
    {
      "vars": {
        "writeKey": "WRITE_KEY",
        "dataPlaneUrl": "DATA_PLANE_URL",
        "pageName": "Nombre de la página"
      },
      "extraUrlParams": {
        "properties.seccion": "economia",
        "properties.autor": "Juan Pérez",
        "properties.article_id": "mi-articulo-123"
      }
    }
  </script>
</amp-analytics>
```

Las propiedades definidas en el nivel superior de `extraUrlParams` se envían con **todos** los eventos de esa página (tanto el `page` automático como cualquier `track` que se configure).

---

## Ejemplo completo

```html
<!doctype html>
<html ⚡>
<head>
  <meta charset="utf-8">
  <title>Mi artículo AMP</title>
  <!-- Componente AMP Analytics -->
  <script async custom-element="amp-analytics"
    src="https://cdn.ampproject.org/v0/amp-analytics-0.1.js"></script>
</head>
<body>
  <amp-analytics config="https://cdn.rudderlabs.com/amp/rudderstack.json">
    <script type="application/json">
      {
        "vars": {
          "writeKey": "WRITE_KEY",
          "dataPlaneUrl": "DATA_PLANE_URL",
          "pageName": "Mi artículo AMP"
        },
        "extraUrlParams": {
          "properties.seccion": "economia",
          "properties.autor": "Juan Pérez",
          "properties.article_id": "mi-articulo-123"
        }
      }
    </script>
  </amp-analytics>

  <h1>Título del artículo</h1>
  <!-- Contenido -->
</body>
</html>
```

---

## Notas para el equipo de desarrollo

- Los eventos llegan al esquema `amp_events` en el destino de Midas. La tabla principal es `amp_events.pages`.
- El `anonymousId` en páginas AMP tiene el formato `amp-<id>` y es **distinto** al `anonymous_id` que genera el SDK de JavaScript en páginas no-AMP. Esto significa que un mismo usuario navegando entre páginas AMP (en caché de Google) y páginas normales del sitio generará dos identidades separadas.
- No incluir el snippet en páginas no-AMP; para esas páginas el tracking ya está cubierto por el SDK de JavaScript de Midas.
