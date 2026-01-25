# Deduplicación

Evita procesar eventos duplicados.

## Deduplicación Básica

```javascript
export default async function(event, { log, store }) {
  const eventId = `${event.user_id}_${event.event}_${event.timestamp}`;
  
  const seen = await store.get(`seen:${eventId}`);
  
  if (seen) {
    log(`Duplicate detected: ${eventId}`);
    return null;
  }
  
  // Marcar como visto (expira en 24h)
  await store.set(`seen:${eventId}`, true, { ttl: 86400 });
  
  return event;
}
```

## Próximos Pasos
- [Notificaciones](notificaciones.md)
- [PII Masking](pii-masking.md)
