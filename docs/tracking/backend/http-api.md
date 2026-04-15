# HTTP API

Envía eventos desde cualquier lenguaje usando HTTP.

## Endpoint

```
POST https://cdp.companyname.m1das.app/api/s/s2s/{event-type}
```

## Headers

```http
Content-Type: application/json
X-Write-Key: cdp.abc123def456.xyz
```

## Body

```json
{
  "event": "event_name",
  "userId": "user_123",
  "timestamp": "2026-01-24T10:30:00.000Z",
  "properties": {
    "property1": "value1"
  }
}
```

## Ejemplos

### cURL

```bash
curl --location 'https://cdp.companyname.m1das.app/api/s/s2s/track' \
--header 'Content-Type: application/json' \
--header 'X-Write-Key: cdp.abc123def456.xyz' \
--data-raw '{
  "type": "track",
  "event": "testEvent",
  "properties": {
    "testProp": "test event properties"
  },
  "userId": "user@example.com",
  "anonymousId": "bKTtbVZw3yiqCJvCSJgjVeXp",
  "timestamp": "2023-04-12T13:29:04.690Z",
  "sentAt": "2023-04-12T13:29:04.690Z",
  "messageId": "voV6fulcZR4CTVnN89AnxFnC",
  "context": {
    "library": {
      "name": "jitsu-js",
      "version": "1.0.0"
    },
    "ip": "127.0.0.1",
    "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/111.0",
    "locale": "en-US",
    "screen": {
      "width": 2304,
      "height": 1296,
      "innerWidth": 1458,
      "innerHeight": 1186,
      "density": 2
    },
    "traits": {
      "email": "user@example.com"
    },
    "page": {
      "path": "/",
      "referrer": "",
      "referring_domain": "",
      "host": "example.com",
      "search": "",
      "title": "Example page event",
      "url": "https://example.com/",
      "encoding": "UTF-8"
    },
    "campaign": {
      "name": "example",
      "source": "g"
    }
  },
  "receivedAt": "2023-04-12T13:29:04.690Z"
}'
```

### Python

```python
import requests

requests.post(
  'https://cdp.companyname.m1das.app/api/s/s2s/{event-type}',
  headers={
    'X-Write-Key': 'cdp.abc123def456.xyz',
    'Content-Type': 'application/json'
  },
  json={
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
$ch = curl_init('https://cdp.companyname.m1das.app/api/s/s2s/{event-type}');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, [
  'Authorization: Bearer s2s.SECRET.HERE',
  'Content-Type: application/json'
]);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode([
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

## Próximos Pasos

- [Node.js SDK](nodejs.md)
- [Python SDK](python.md)
