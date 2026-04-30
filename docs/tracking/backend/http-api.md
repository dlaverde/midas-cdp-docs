# HTTP API

Envía eventos desde cualquier lenguaje o plataforma usando HTTP directo. Útil para integraciones de backend sin SDK.

## Autenticación

### Write Key (recomendado)

Incluye el header `X-Write-Key` con el write key de tu sitio:

```http
X-Write-Key: keyId:keySecret
```

### Autenticación básica

También se soporta autenticación HTTP Basic donde el Write Key actúa como `username` y el `password` se deja vacío (el `:` al final es obligatorio):

```
writeKey123:
```

Después de codificar en base64:

```http
Authorization: Basic d3JpdGVLZXkxMjM6Cg==
```

### Query parameter

Puedes pasar el write key como parámetro en la URL. Útil para pruebas, pero **no recomendado en producción**:

```
https://cdp.companyname.m1das.app/api/s/{event-type}?writekey=keyId:keySecret
```

---

## Endpoint de ingesta

```
POST https://cdp.companyname.m1das.app/api/s/{event-type}
```

Acepta eventos en formato JSON. Funciona tanto para eventos de browser como server-to-server según el tipo de Write Key.

`{event-type}` puede ser:

| Valor | Descripción |
|-------|-------------|
| `page` | Vista de página |
| `track` | Evento personalizado |
| `identify` | Identificación de usuario |
| `group` | Agrupación de usuarios |
| `event` | El servidor toma el tipo desde el campo `type` del payload |

---

## Ejemplos

### Evento `page`

```bash
curl --location 'https://cdp.companyname.m1das.app/api/s/page' \
--header 'Content-Type: application/json' \
--header 'X-Write-Key: keyId:keySecret' \
--data-raw '{
  "type": "page",
  "properties": {
    "title": "Ejemplo de página",
    "url": "https://example.com/",
    "path": "/",
    "hash": "",
    "search": "",
    "width": 1458,
    "height": 1186
  },
  "userId": "user@example.com",
  "anonymousId": "dBRu6l026JMy7mmUewl5WgCM",
  "timestamp": "2023-04-12T13:28:02.531Z",
  "sentAt": "2023-04-12T13:28:02.531Z",
  "messageId": "GBzdRBFz48ZnuUyASrVYUMKJ",
  "context": {
    "ip": "127.0.0.1",
    "userAgent": "Mozilla/5.0 ...",
    "locale": "en-US",
    "page": {
      "path": "/",
      "referrer": "",
      "host": "example.com",
      "title": "Ejemplo de página",
      "url": "https://example.com/"
    }
  }
}'
```

### Evento `identify`

```bash
curl --location 'https://cdp.companyname.m1das.app/api/s/identify' \
--header 'Content-Type: application/json' \
--header 'X-Write-Key: keyId:keySecret' \
--data-raw '{
  "type": "identify",
  "userId": "user@example.com",
  "traits": {
    "email": "user@example.com"
  },
  "anonymousId": "aTc2kpU1m9gMARgq9RAizRyj",
  "timestamp": "2023-04-12T13:28:47.743Z",
  "sentAt": "2023-04-12T13:28:47.743Z",
  "messageId": "PgLUzb855vhdmhROLXXGy9zP",
  "context": {
    "ip": "127.0.0.1",
    "userAgent": "Mozilla/5.0 ...",
    "locale": "en-US"
  }
}'
```

### Evento `track`

```bash
curl --location 'https://cdp.companyname.m1das.app/api/s/track' \
--header 'Content-Type: application/json' \
--header 'X-Write-Key: keyId:keySecret' \
--data-raw '{
  "type": "track",
  "event": "purchase_completed",
  "properties": {
    "order_id": "ORD-456",
    "total": 99.99
  },
  "userId": "user@example.com",
  "anonymousId": "bKTtbVZw3yiqCJvCSJgjVeXp",
  "timestamp": "2023-04-12T13:29:04.690Z",
  "sentAt": "2023-04-12T13:29:04.690Z",
  "messageId": "voV6fulcZR4CTVnN89AnxFnC",
  "context": {
    "ip": "127.0.0.1",
    "userAgent": "Mozilla/5.0 ...",
    "locale": "en-US",
    "page": {
      "path": "/checkout",
      "url": "https://example.com/checkout"
    }
  }
}'
```

### Python

```python
import requests

requests.post(
  'https://cdp.companyname.m1das.app/api/s/track',
  headers={
    'X-Write-Key': 'keyId:keySecret',
    'Content-Type': 'application/json'
  },
  json={
    'type': 'track',
    'event': 'order_completed',
    'userId': 'user_123',
    'properties': {
      'order_id': 'ORD-456',
      'total': 99.99
    }
  }
)
```

### PHP

```php
<?php
$ch = curl_init('https://cdp.companyname.m1das.app/api/s/track');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  'X-Write-Key: keyId:keySecret',
  'Content-Type: application/json'
]);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
  'type' => 'track',
  'event' => 'order_completed',
  'userId' => 'user_123',
  'properties' => [
    'order_id' => 'ORD-456',
    'total' => 99.99
  ]
]));
curl_exec($ch);
?>
```

---

## Endpoint batch

Envía múltiples eventos en una sola solicitud. Compatible con el formato batch de Segment.

```
POST https://cdp.companyname.m1das.app/v1/batch
```

```json
{
  "batch": [
    {
      "type": "page",
      "properties": {
        "title": "Ejemplo de página",
        "url": "https://example.com/"
      },
      "userId": "user@example.com",
      "timestamp": "2023-04-12T13:28:02.531Z"
    },
    {
      "type": "track",
      "event": "button_clicked",
      "userId": "user@example.com",
      "properties": {
        "button": "signup"
      },
      "timestamp": "2023-04-12T13:28:05.000Z"
    }
  ],
  "writeKey": "keyId:keySecret",
  "context": {
    "device": {
      "type": "desktop"
    }
  }
}
```

| Campo | Descripción |
|-------|-------------|
| `batch` | Array JSON de eventos |
| `writeKey` | Write Key del sitio |
| `context` | Contexto opcional que se mezcla con cada evento |

---

## Próximos Pasos

- [Node.js SDK](nodejs.md)
- [Python SDK](python.md)
