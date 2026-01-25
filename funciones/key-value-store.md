# Key-Value Store

Almacenamiento persistente para funciones.

## Uso Básico

```javascript
export default async function(event, { store }) {
  // Leer
  const value = await store.get('key');
  
  // Escribir
  await store.set('key', 'value');
  
  // Eliminar
  await store.delete('key');
  
  return event;
}
```

## Ejemplo: Stats de Usuario

```javascript
export default async function(event, { store, log }) {
  const userId = event.user_id;
  
  // Leer stats
  const stats = await store.get(`user:${userId}:stats`) || {
    total_events: 0,
    first_seen: event.timestamp,
    last_seen: event.timestamp
  };
  
  // Actualizar
  stats.total_events += 1;
  stats.last_seen = event.timestamp;
  
  // Guardar
  await store.set(`user:${userId}:stats`, stats);
  
  // Agregar al evento
  event.user_stats = stats;
  
  return event;
}
```

## TTL (Time To Live)

```javascript
// Expira en 24 horas
await store.set('key', 'value', { ttl: 86400 });
```

## Próximos Pasos
- [Ejemplos de Transformaciones](ejemplos.md)
- [NPM Packages](npm-packages.md)
