# Testing

Prueba tu implementación de tracking.

## Test en Desarrollo

```javascript
const analytics = jitsuClient({
  key: process.env.NODE_ENV === 'production' 
    ? 'js.prod.key.here'
    : 'js.dev.key.here'
});
```

## Dry Run Mode

```javascript
const analytics = jitsuClient({
  key: 'js.your.key',
  debug: true,
  dry_run: true // No envía eventos
});
```

## Validación de Eventos

```javascript
function validateEvent(eventName, properties) {
  const required = trackingPlan[eventName]?.required || [];
  
  for (const prop of required) {
    if (!properties[prop]) {
      console.error(`Missing: ${prop}`);
      return false;
    }
  }
  
  return true;
}

// Uso
if (validateEvent('Product Purchased', { product_id, price })) {
  analytics.track('Product Purchased', { product_id, price });
}
```

## Próximos Pasos
- [Monitoring](monitoring.md)
- [Funciones](../funciones/introduccion.md)
