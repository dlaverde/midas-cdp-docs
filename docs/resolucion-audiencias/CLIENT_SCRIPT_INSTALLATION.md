# Guia de Instalacion del Script de Audiencias

Este documento explica como instalar y usar el script de audiencias en un sitio web cliente.

El script consulta audiencias e intereses asociados a un identificador anonimo del visitante y deja esa informacion disponible para que el sitio pueda usarla en personalizacion, pauta, analitica u otras integraciones propias.

## Que Hace el Script

El script realiza el siguiente flujo en el navegador:

1. Busca la cookie `__eventn_id` en el sitio.
2. Usa ese valor como identificador anonimo del visitante.
3. Hace una peticion al servicio de resolucion de audiencias.
4. Recibe las audiencias e intereses asociados a ese visitante.
5. Deja la respuesta disponible en variables globales de `window`.
6. Dispara un evento personalizado para que otros scripts puedan capturar la respuesta.

El script esta disenado para no bloquear la carga del sitio. Si no encuentra el identificador anonimo, si la peticion falla o si el servicio no responde a tiempo, el sitio continua funcionando normalmente.

## Manejo de la API Key

El script incluye un valor configurable para autenticar la peticion:

```js
const API_KEY = "TU_API_KEY";
```

Importante: no se debe incluir una API key privada o sensible directamente en codigo frontend. Todo valor incluido en un script del navegador puede ser visto por usuarios, herramientas de desarrollo, proxies, logs de red o terceros con acceso al sitio.

Para entornos productivos, se recomienda usar una de estas alternativas:

- Usar un token publico restringido, emitido exclusivamente para uso desde navegador.
- Usar un token con permisos limitados solo para consulta de audiencias.
- Usar tokens de corta duracion generados por un backend del cliente.
- Hacer que el sitio llame a un endpoint propio del cliente y que ese backend agregue las credenciales necesarias.

Si se entrega un token para usar directamente en el script, ese token debe tratarse como publico y no como secreto.

## Donde Instalar el Script

El script debe instalarse dentro del `<head>` del sitio web, preferiblemente lo mas arriba posible despues de los scripts que crean la cookie `__eventn_id`, si existen.

Ejemplo:

```html
<head>
  <!-- Otros scripts requeridos por el sitio -->

  <script src="https://cdn.example.com/scriptHead.js" async></script>
</head>
```

Tambien puede instalarse inline si el cliente recibe el contenido completo del archivo:

```html
<head>
  <script>
    (function () {
      // Contenido del script entregado
    })();
  </script>
</head>
```

## Configuracion Basica

Antes de instalarlo, se deben revisar estos valores dentro del script:

```js
const RESOLVER_URL = "https://resolver.rcnaudiences.com/resolve";
const API_KEY = "TU_API_KEY";
```

`RESOLVER_URL` corresponde al servicio que entrega las audiencias.

`API_KEY` debe reemplazarse solo por el token o mecanismo de autenticacion acordado para el cliente. No debe usarse una credencial privada en frontend.

## Respuesta Esperada

El script espera recibir una respuesta JSON con esta estructura:

```json
{
  "anonymous_id": "e2f5d9a9-14eb-4b93-a403-d17eb0412872",
  "audiences": ["aud:rcn:test-interests"],
  "interests": ["noticias", "mundo", "colombia"]
}
```

Campos:

- `anonymous_id`: identificador anonimo usado para resolver la informacion.
- `audiences`: lista de audiencias asociadas al visitante.
- `interests`: lista de intereses asociados al visitante.

Si el visitante no tiene audiencias o intereses disponibles, los arreglos pueden venir vacios.

## Como Capturar la Respuesta

Cuando el script recibe una respuesta exitosa, guarda los datos en estas variables globales:

```js
window.__MIDAS_AUDIENCES__;
window.__MIDAS_INTERESTS__;
window.__MIDAS_RESOLVER_RESPONSE__;
```

Ejemplo de uso:

```html
<script>
  console.log(window.__MIDAS_AUDIENCES__);
  console.log(window.__MIDAS_INTERESTS__);
  console.log(window.__MIDAS_RESOLVER_RESPONSE__);
</script>
```

Como la peticion ocurre de forma asincrona, la forma recomendada de consumir la respuesta es escuchar el evento `midas:audiences-ready`:

```html
<script>
  window.addEventListener("midas:audiences-ready", function (event) {
    const data = event.detail;

    console.log("Anonymous ID:", data.anonymous_id);
    console.log("Audiences:", data.audiences);
    console.log("Interests:", data.interests);
  });
</script>
```

## Ejemplo de Uso en el Sitio

El cliente puede usar las audiencias para activar logica propia:

```html
<script>
  window.addEventListener("midas:audiences-ready", function (event) {
    const audiences = event.detail.audiences || [];
    const interests = event.detail.interests || [];

    if (audiences.includes("aud:rcn:test-interests")) {
      console.log("Visitor belongs to test-interests audience");
    }

    if (interests.includes("noticias")) {
      console.log("Visitor has noticias interest");
    }
  });
</script>
```

## Recomendacion de Orden

Si otro script del cliente necesita usar las audiencias, debe escuchar el evento antes o justo despues de cargar el script de audiencias:

```html
<head>
  <script>
    window.addEventListener("midas:audiences-ready", function (event) {
      window.CLIENT_AUDIENCE_DATA = event.detail;
    });
  </script>

  <script src="https://cdn.example.com/scriptHead.js" async></script>
</head>
```

De esta forma, el sitio puede reaccionar apenas la informacion este disponible.
