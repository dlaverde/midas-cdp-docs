# Documentacion Tecnica — Integracion con Audience Resolver

Este documento describe como implementar, desde el lado del cliente, un script en el navegador que consulte el servicio de resolucion de audiencias. El cliente puede usar esta guia para escribir su propia integracion sin depender de un snippet predefinido.

## Resumen del Flujo

```text
1. Leer cookie __eventn_id del sitio
2. Construir URL: GET /resolve?anon=<anonymous_id>
3. Enviar peticion con header x-api-key
4. Recibir JSON con audiences e interests
5. Usar la respuesta en la logica del sitio
```

El identificador anonimo proviene de la cookie del visitante. El servicio devuelve las audiencias e intereses asociados a ese ID.

## Identificador Anonimo (Cookie)

### Nombre de la cookie

```text
__eventn_id
```

Este valor se usa como `anonymous_id` en la peticion al resolver.

### Requisitos

- La cookie debe existir en el dominio del sitio donde se ejecuta el script.
- Debe ser legible por JavaScript (`document.cookie`). Si la cookie tiene flag `HttpOnly`, no podra leerse desde el navegador y esta integracion no funcionara sin otro mecanismo (por ejemplo, un endpoint backend del cliente).
- El valor suele ser un UUID, por ejemplo: `e2f5d9a9-14eb-4b93-a403-d17eb0412872`.

### Lectura de la cookie

Funcion basica para obtener el valor:

```js
/**
 * Read a cookie value by name.
 * @param {string} name
 * @returns {string|null}
 */
function getCookie(name) {
  const match = document.cookie.match(
    new RegExp("(^|;\\s*)" + name + "=([^;]*)")
  );

  return match ? decodeURIComponent(match[2]) : null;
}

const anonymousId = getCookie("__eventn_id");
```

### Esperar a que la cookie exista

En muchos sitios la cookie `__eventn_id` se crea de forma asincrona por otro script (CDP, tag manager, etc.). Si el script de audiencias corre antes de que exista la cookie, la lectura fallara.

Se recomienda reintentar durante un periodo corto antes de abandonar:

```js
/**
 * Wait until __eventn_id cookie is available.
 * @param {number} maxRetries
 * @param {number} intervalMs
 * @returns {Promise<string|null>}
 */
async function waitForAnonymousId(maxRetries, intervalMs) {
  for (let i = 0; i < maxRetries; i++) {
    const anonymousId = getCookie("__eventn_id");

    if (anonymousId) {
      return anonymousId;
    }

    await new Promise(function (resolve) {
      setTimeout(resolve, intervalMs);
    });
  }

  return null;
}
```

Valores recomendados:

| Parametro      | Valor sugerido | Descripcion                          |
|----------------|----------------|--------------------------------------|
| `maxRetries`   | 10             | Numero maximo de intentos            |
| `intervalMs`   | 300            | Milisegundos entre intentos          |
| Tiempo total   | ~3 segundos    | Ventana maxima de espera de la cookie |

Si despues de los reintentos no hay cookie, el script debe terminar sin bloquear el sitio.

## Endpoint de Resolucion

### URL base

```text
https://resolver.rcnaudiences.com/resolve
```

La URL exacta de produccion sera confirmada al momento de la integracion.

### Metodo HTTP

```text
GET
```

### Query parameters

| Parametro | Requerido | Descripcion                                      |
|-----------|-----------|--------------------------------------------------|
| `anon`    | Si        | Valor de la cookie `__eventn_id`, URL-encoded    |

Ejemplo:

```text
GET https://resolver.rcnaudiences.com/resolve?anon=e2f5d9a9-14eb-4b93-a403-d17eb0412872
```

### Headers requeridos

| Header       | Requerido | Descripcion                              |
|--------------|-----------|------------------------------------------|
| `x-api-key`  | Si        | Token de autenticacion entregado al cliente |

No se requiere `Content-Type` en peticiones GET.

### Headers recomendados en el cliente

| Opcion / Header   | Valor sugerido   | Motivo                                      |
|-------------------|------------------|---------------------------------------------|
| `cache`           | `no-store`       | Evitar respuestas cacheadas por el navegador |
| `credentials`     | `omit`           | No enviar cookies del sitio al resolver      |

### Ejemplo con fetch

```js
const RESOLVER_URL = "https://resolver.rcnaudiences.com/resolve";
const API_KEY = "TOKEN_ENTREGADO_AL_CLIENTE";

const anonymousId = await waitForAnonymousId(10, 300);

if (!anonymousId) {
  console.warn("[Audience Resolver] No anonymous id found");
  return;
}

const url =
  RESOLVER_URL + "?anon=" + encodeURIComponent(anonymousId);

const response = await fetch(url, {
  method: "GET",
  headers: {
    "x-api-key": API_KEY
  },
  credentials: "omit",
  cache: "no-store"
});
```

### Autenticacion (API Key)

Toda peticion a `/resolve` debe incluir el header `x-api-key`.

**Importante:** cualquier valor incluido en codigo JavaScript del navegador es visible publicamente. No debe usarse una credencial privada de backend. Opciones recomendadas:

- Token publico restringido, emitido solo para consulta desde navegador.
- Token con permisos limitados al endpoint `/resolve`.
- Proxy en backend del cliente: el navegador llama a un endpoint propio y el servidor agrega la autenticacion.

Si el token se incluye en frontend, debe tratarse como publico, no como secreto.

## Respuesta Exitosa

### Codigo HTTP

```text
200 OK
```

### Content-Type

```text
application/json; charset=utf-8
```

### Estructura del body

```json
{
  "anonymous_id": "e2f5d9a9-14eb-4b93-a403-d17eb0412872",
  "audiences": ["aud:rcn:test-interests"],
  "interests": ["noticias", "mundo", "colombia"]
}
```

### Campos

| Campo           | Tipo     | Descripcion                                                |
|-----------------|----------|------------------------------------------------------------|
| `anonymous_id`  | string   | Mismo valor enviado en el query param `anon`               |
| `audiences`     | string[] | Lista de audiencias del visitante. Puede ser `[]`           |
| `interests`     | string[] | Lista de intereses del visitante. Puede ser `[]`            |

### Formato de audiencias

Cada elemento de `audiences` sigue este patron:

```text
aud:<client_id>:<audience_slug>
```

Ejemplo:

```text
aud:rcn:test-interests
```

- `client_id`: identificador del cliente en la plataforma.
- `audience_slug`: slug de la audiencia.

### Comportamiento cuando no hay datos

Si el visitante no tiene audiencias o intereses registrados, el servicio responde `200` con arreglos vacios:

```json
{
  "anonymous_id": "e2f5d9a9-14eb-4b93-a403-d17eb0412872",
  "audiences": [],
  "interests": []
}
```

Esto no es un error. El cliente debe manejar arreglos vacios como caso valido.

## Codigos de Respuesta HTTP

| Codigo | Significado              | Body tipico                              | Accion recomendada del cliente        |
|--------|--------------------------|------------------------------------------|---------------------------------------|
| `200`  | Exito                    | JSON con `anonymous_id`, `audiences`, `interests` | Parsear y usar la respuesta    |
| `400`  | Parametro faltante       | `{ "error": "Missing query param: anon" }` | Verificar que `anon` se envie correctamente |
| `401`  | No autorizado            | `{ "error": "Unauthorized" }`            | Revisar valor de `x-api-key`          |
| `500`  | Error interno del servicio | `{ "error": "Internal server error" }` | Reintentar o fallar silenciosamente   |

### Errores de red y timeout

El cliente debe contemplar estos casos fuera de los codigos HTTP:

| Situacion              | Comportamiento tipico en fetch     | Accion recomendada                    |
|------------------------|------------------------------------|---------------------------------------|
| Timeout                | `AbortError` o promise rechazada   | No bloquear el sitio; log opcional    |
| Sin conexion           | Error de red                       | Fallar silenciosamente                |
| CORS bloqueado         | Error en consola del navegador     | Contactar al proveedor del resolver   |
| JSON invalido          | Error al parsear `response.json()` | Tratar como fallo de integracion      |

Se recomienda un timeout de **1500 ms** a **3000 ms** para no afectar la carga del sitio.

### Ejemplo de manejo de respuesta

```js
if (!response.ok) {
  if (response.status === 401) {
    console.warn("[Audience Resolver] Invalid API key");
  } else if (response.status === 400) {
    console.warn("[Audience Resolver] Bad request");
  } else {
    console.warn("[Audience Resolver] HTTP error", response.status);
  }
  return;
}

const data = await response.json();

const audiences = data.audiences || [];
const interests = data.interests || [];
```

## CORS (Navegador)

Las peticiones desde JavaScript en el navegador hacia un dominio distinto al del sitio requieren que el servicio permita el origen del cliente.

El navegador enviara una peticion preflight `OPTIONS` antes del `GET` porque se usa el header personalizado `x-api-key`. El servicio responde `204 No Content` al preflight cuando el origen esta permitido.

Desde el lado del cliente:

- La integracion debe ejecutarse en el dominio acordado (por ejemplo `https://www.ejemplo.com`).
- Si aparece un error de CORS en consola, el dominio del sitio debe ser autorizado por el proveedor del resolver.

## Implementacion de Referencia Completa

Ejemplo minimo listo para adaptar:

```js
(function () {
  const RESOLVER_URL = "https://resolver.rcnaudiences.com/resolve";
  const API_KEY = "TOKEN_ENTREGADO_AL_CLIENTE";
  const REQUEST_TIMEOUT_MS = 1500;
  const MAX_COOKIE_RETRIES = 10;
  const COOKIE_RETRY_INTERVAL_MS = 300;

  /**
   * Read cookie value by name.
   * @param {string} name
   * @returns {string|null}
   */
  function getCookie(name) {
    const match = document.cookie.match(
      new RegExp("(^|;\\s*)" + name + "=([^;]*)")
    );

    return match ? decodeURIComponent(match[2]) : null;
  }

  /**
   * Sleep helper.
   * @param {number} ms
   * @returns {Promise<void>}
   */
  function sleep(ms) {
    return new Promise(function (resolve) {
      setTimeout(resolve, ms);
    });
  }

  /**
   * Fetch with timeout.
   * @param {string} url
   * @param {RequestInit} options
   * @param {number} timeoutMs
   * @returns {Promise<Response>}
   */
  async function fetchWithTimeout(url, options, timeoutMs) {
    const controller = new AbortController();
    const timeout = setTimeout(function () {
      controller.abort();
    }, timeoutMs);

    try {
      return await fetch(url, {
        ...options,
        signal: controller.signal
      });
    } finally {
      clearTimeout(timeout);
    }
  }

  /**
   * Wait until __eventn_id cookie exists.
   * @returns {Promise<string|null>}
   */
  async function waitForAnonymousId() {
    for (let i = 0; i < MAX_COOKIE_RETRIES; i++) {
      const anonymousId = getCookie("__eventn_id");

      if (anonymousId) {
        return anonymousId;
      }

      await sleep(COOKIE_RETRY_INTERVAL_MS);
    }

    return null;
  }

  /**
   * Resolve audiences and interests for the current visitor.
   * @returns {Promise<object|null>}
   */
  async function resolveAudiences() {
    const anonymousId = await waitForAnonymousId();

    if (!anonymousId) {
      return null;
    }

    const url =
      RESOLVER_URL + "?anon=" + encodeURIComponent(anonymousId);

    const response = await fetchWithTimeout(
      url,
      {
        method: "GET",
        headers: {
          "x-api-key": API_KEY
        },
        credentials: "omit",
        cache: "no-store"
      },
      REQUEST_TIMEOUT_MS
    );

    if (!response.ok) {
      throw new Error("Resolver HTTP " + response.status);
    }

    return response.json();
  }

  /**
   * Bootstrap client integration.
   */
  async function init() {
    try {
      const data = await resolveAudiences();

      if (!data) {
        return;
      }

      // Opcion A: variables globales
      window.CLIENT_AUDIENCES = data.audiences || [];
      window.CLIENT_INTERESTS = data.interests || [];

      // Opcion B: evento personalizado
      window.dispatchEvent(
        new CustomEvent("audiences:ready", {
          detail: data
        })
      );
    } catch (err) {
      // Fallar silenciosamente: no romper render ni pauta
      console.warn("[Audience Resolver] Integration failed", err);
    }
  }

  init();
})();
```

## Como Consumir la Respuesta en el Sitio

### Opcion 1: Evento personalizado (recomendado)

Registrar el listener antes o al cargar el script de integracion:

```html
<script>
  window.addEventListener("audiences:ready", function (event) {
    const data = event.detail;

    console.log("Anonymous ID:", data.anonymous_id);
    console.log("Audiences:", data.audiences);
    console.log("Interests:", data.interests);
  });
</script>
```

### Opcion 2: Variables globales

```js
if (window.CLIENT_AUDIENCES && window.CLIENT_AUDIENCES.length > 0) {
  // usar audiencias
}
```

Como la peticion es asincrona, evitar leer variables globales inmediatamente despues de incluir el script. Preferir el evento.

### Opcion 3: Promise / callback propio

El cliente puede envolver `resolveAudiences()` en su propia capa:

```js
resolveAudiences()
  .then(function (data) {
    if (!data) return;
    activatePersonalization(data);
  })
  .catch(function () {
    // fallback silencioso
  });
```

## Ejemplos de Logica de Negocio

### Verificar pertenencia a una audiencia

```js
function belongsToAudience(audiences, clientId, slug) {
  const target = "aud:" + clientId + ":" + slug;
  return audiences.indexOf(target) !== -1;
}

// Uso
if (belongsToAudience(data.audiences, "rcn", "test-interests")) {
  // logica para visitantes de esa audiencia
}
```

### Verificar interes

```js
if (data.interests.indexOf("noticias") !== -1) {
  // logica para interes en noticias
}
```

## Donde Instalar el Script

Colocar el script en el `<head>` del sitio, preferiblemente despues de los tags que crean `__eventn_id`:

```html
<head>
  <script>
    window.addEventListener("audiences:ready", function (event) {
      window.CLIENT_AUDIENCE_DATA = event.detail;
    });
  </script>

  <script src="/js/audience-resolver-integration.js" async></script>
</head>
```

Si se usa `async`, el script puede ejecutarse en cualquier momento. Los reintentos de cookie mitigan el caso en que `__eventn_id` aun no exista.

## Buenas Practicas

1. **No bloquear la pagina:** capturar errores y continuar aunque falle la resolucion.
2. **Timeout corto:** 1.5–3 s maximo.
3. **No loguear el API key** en consola ni en herramientas de analitica.
4. **Tratar arrays vacios como validos:** un visitante sin audiencias es respuesta normal.
5. **Codificar `anon`:** siempre usar `encodeURIComponent(anonymousId)` en la URL.
6. **Una sola peticion por pagina** salvo que el flujo de negocio requiera otra cosa.

## Prueba Manual (curl)

Para validar conectividad y token fuera del navegador:

```bash
curl -sS \
  -H "x-api-key: TOKEN_ENTREGADO_AL_CLIENTE" \
  "https://resolver.rcnaudiences.com/resolve?anon=e2f5d9a9-14eb-4b93-a403-d17eb0412872"
```

Respuesta esperada:

```json
{
  "anonymous_id": "e2f5d9a9-14eb-4b93-a403-d17eb0412872",
  "audiences": ["aud:rcn:test-interests"],
  "interests": ["noticias", "mundo", "colombia"]
}
```

`curl` no valida CORS; sirve para probar autenticacion y formato de respuesta. La integracion en navegador debe probarse en el dominio real del sitio.

## Checklist de Integracion

- [ ] Cookie `__eventn_id` disponible y legible en el dominio del sitio
- [ ] Token `x-api-key` configurado (publico/restringido o via proxy backend)
- [ ] Dominio del sitio autorizado para CORS
- [ ] Script instalado en `<head>` con manejo asincrono de respuesta
- [ ] Manejo de codigos `400`, `401`, `500` y errores de red/timeout
- [ ] Prueba en navegador con visitante con y sin audiencias registradas
