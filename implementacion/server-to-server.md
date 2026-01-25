# Server-to-Server (HTTP API)

Para backends, APIs, y sistemas que no pueden usar JavaScript.

## Endpoint

```
POST https://tracking.midas.com/api/v1/s2s/event
```

## Headers

```http
Content-Type: application/json
X-Auth-Token: s2s.TU_SERVER_SECRET.AQUI
```

## Payload

```json
{
  "event_type": "track",
  "event": "order_completed",
  "user_id": "user_123",
  "properties": {
    "order_id": "ORD-789",
    "total": 299.99
  }
}
```

## Ejemplos por Lenguaje

- [Python](server-to-server/python.md)
- [Node.js](server-to-server/nodejs.md)
- [PHP](server-to-server/php.md)
- [Ruby](server-to-server/ruby.md)
- [Go](server-to-server/go.md)

## Batch Events

```json
{
  "batch": [
    {"event": "page_view", ...},
    {"event": "button_click", ...}
  ]
}
```

## Próximos Pasos
- [Segment Compatibility](segment.md)
- [Node.js Server-Side](nodejs-server-side.md)
