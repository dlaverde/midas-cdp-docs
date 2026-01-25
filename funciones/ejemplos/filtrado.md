# Filtrado de Eventos

Filtra eventos no deseados antes de almacenarlos.

## Filtrar Tráfico Interno

```javascript
export default async function(event, { log }) {
  const internalIPs = ['192.168.1.0/24', '10.0.0.0/8'];
  const ip = event.context?.ip;
  
  if (isInternalIP(ip, internalIPs)) {
    log(`Filtering internal IP: ${ip}`);
    return null; // null = no enviar evento
  }
  
  return event;
}

function isInternalIP(ip, ranges) {
  // Lógica de validación
  return false; // implementar
}
```

## Filtrar Bots

```javascript
export default async function(event, { log }) {
  const userAgent = event.context?.userAgent;
  const botPatterns = /bot|crawler|spider|scraper/i;
  
  if (botPatterns.test(userAgent)) {
    log('Bot detected, filtering');
    return null;
  }
  
  return event;
}
```

## Próximos Pasos
- [Enriquecimiento](enriquecimiento.md)
- [Normalización](normalizacion.md)
