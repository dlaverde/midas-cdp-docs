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

Agrega la siguiente línea antes del cierre de la etiqueta `</head>` de tu página AMP:

```html
<script async custom-element="amp-analytics"
  src="https://cdn.ampproject.org/v0/amp-analytics-0.1.js"></script>
```

---

## Paso 2 — Agregar el bloque de configuración

Agrega el siguiente bloque dentro de tu etiqueta `<body>`, reemplazando `WRITE_KEY`, `DATA_PLANE_URL` y el nombre de la página:

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

---

## Evento Page

El componente incluye un page view automático al cargar la página. Puedes configurar el nombre mediante la variable `pageName`:

```json
"vars": {
  "writeKey": "WRITE_KEY",
  "dataPlaneUrl": "DATA_PLANE_URL",
  "pageName": "Nombre de la página"
}
```

Si no defines `pageName`, el evento se registrará con el nombre `Unknown Page`.

---

## Evento Track

Para registrar eventos de interacción del usuario (clics, scroll, visibilidad de elementos, etc.), usa la sección `triggers`. Define el nombre del evento en `vars.eventName` y apunta el `request` a `track`:

```html
<body>
  <amp-analytics config="https://cdn.rudderlabs.com/amp/rudderstack.json">
    <script type="application/json">
      {
        "vars": {
          "writeKey": "WRITE_KEY",
          "dataPlaneUrl": "DATA_PLANE_URL",
          "pageName": "Mi página AMP"
        },
        "triggers": {
          "clickEnBoton": {
            "on": "click",
            "selector": "#cta-boton",
            "request": "track",
            "vars": {
              "eventName": "cta_click"
            },
            "extraUrlParams": {
              "properties.tipo_clic": "boton_primario"
            }
          }
        }
      }
    </script>
  </amp-analytics>

  <!-- Elemento que dispara el evento -->
  <button id="cta-boton">Suscríbete</button>
</body>
```

Puedes definir múltiples triggers dentro del mismo bloque. Cada trigger puede tener su propio `eventName` y sus propias `extraUrlParams`.

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

## Paso 4 (opcional) — Propiedades personalizadas

Puedes enriquecer los eventos con metadatos del contenido usando `extraUrlParams`. Toda propiedad debe llevar el prefijo `properties.`.

Existen dos niveles:

- **A nivel raíz:** se envían con **todos** los eventos de la página (el `page` automático y cualquier `track`).
- **Dentro de un trigger:** se envían **solo** con ese evento específico.

### Propiedades globales (para todos los eventos)

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

### Propiedades por evento específico

```html
<amp-analytics config="https://cdn.rudderlabs.com/amp/rudderstack.json">
  <script type="application/json">
    {
      "vars": {
        "writeKey": "WRITE_KEY",
        "dataPlaneUrl": "DATA_PLANE_URL",
        "pageName": "Mi página AMP"
      },
      "triggers": {
        "clickEnlace": {
          "on": "click",
          "selector": "#enlace-1",
          "request": "track",
          "vars": { "eventName": "enlace_click" },
          "extraUrlParams": {
            "properties.destino": "pagina-producto"
          }
        }
      },
      "extraUrlParams": {
        "properties.seccion": "home",
        "properties.article_id": "art-001"
      }
    }
  </script>
</amp-analytics>
```

En este ejemplo, `seccion` y `article_id` se envían en **todos** los eventos, mientras que `destino` solo se envía en el evento `enlace_click`.

---

## Parámetros UTM

AMP no captura automáticamente los parámetros UTM. Debes pasarlos manualmente usando `extraUrlParams`:

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
        "properties.utm_source": "google",
        "properties.utm_medium": "cpc",
        "properties.utm_campaign": "verano-2025"
      }
    }
  </script>
</amp-analytics>
```

---

## AMP Linker (sesión unificada)

Cuando un usuario navega desde una página AMP en caché (p. ej., Google AMP Cache) hacia una página AMP en tu propio dominio, el AMP Client ID puede cambiar, generando dos identidades separadas. Para mantener la continuidad de sesión, activa el **AMP Linker**:

```html
<body>
  <amp-analytics config="https://cdn.rudderlabs.com/amp/rudderstack.json">
    <script type="application/json">
      {
        "vars": {
          "writeKey": "WRITE_KEY",
          "dataPlaneUrl": "DATA_PLANE_URL",
          "pageName": "Mi página AMP"
        },
        "linkers": {
          "enabled": true
        }
      }
    </script>
  </amp-analytics>
</body>
```

Con el linker activado, el AMP Client ID se propaga como parámetro en los enlaces salientes y se usa para establecer una cookie de primera parte en tu dominio, permitiendo identificar al mismo usuario en páginas AMP cacheadas y en páginas AMP propias.

> **Nota:** Para unificar la identidad entre páginas AMP y páginas normales (no-AMP), es necesario integrar adicionalmente el SDK de JavaScript de Midas en las páginas no-AMP y leer el parámetro del linker desde allí.

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
        "triggers": {
          "clickCompartir": {
            "on": "click",
            "selector": "#btn-compartir",
            "request": "track",
            "vars": {
              "eventName": "articulo_compartido"
            },
            "extraUrlParams": {
              "properties.red_social": "twitter"
            }
          }
        },
        "extraUrlParams": {
          "properties.seccion": "economia",
          "properties.autor": "Juan Pérez",
          "properties.article_id": "mi-articulo-123",
          "properties.utm_source": "newsletter",
          "properties.utm_medium": "email"
        },
        "linkers": {
          "enabled": true
        }
      }
    </script>
  </amp-analytics>

  <h1>Título del artículo</h1>
  <button id="btn-compartir">Compartir en Twitter</button>
  <!-- Contenido -->
</body>
</html>
```

---

## Notas para el equipo de desarrollo

- Los eventos llegan al esquema `amp_events` en el destino de Midas. La tabla principal es `amp_events.pages`.
- El `anonymousId` en páginas AMP tiene el formato `amp-<id>` y es distinto al `anonymous_id` que genera el SDK de JavaScript en páginas no-AMP. Esto significa que un mismo usuario navegando entre páginas AMP (en caché de Google) y páginas normales del sitio generará dos identidades separadas; el AMP Linker mitiga esto entre páginas AMP, pero no entre AMP y no-AMP.
- No incluir el snippet en páginas no-AMP; para esas páginas el tracking ya está cubierto por el SDK de JavaScript de Midas.
- Los UTM no se capturan automáticamente; deben enviarse explícitamente vía `extraUrlParams`.
