# Normalización

Normaliza datos para consistencia.

## Normalizar Email

```javascript
export default async function(event) {
  // Email a lowercase
  if (event.traits?.email) {
    event.traits.email = event.traits.email.toLowerCase().trim();
  }
  
  if (event.properties?.email) {
    event.properties.email = event.properties.email.toLowerCase().trim();
  }
  
  return event;
}
```

## Normalizar Eventos

```javascript
export default async function(event) {
  // Normalizar nombre de evento
  if (event.event) {
    event.event = event.event
      .toLowerCase()
      .replace(/\s+/g, '_')
      .replace(/[^a-z0-9_]/g, '');
  }
  
  // Agregar timestamp si falta
  if (!event.timestamp) {
    event.timestamp = new Date().toISOString();
  }
  
  return event;
}
```

## Próximos Pasos
- [Deduplicación](deduplicacion.md)
- [PII Masking](pii-masking.md)
