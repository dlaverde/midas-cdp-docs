# JavaScript SDK

El SDK de JavaScript es la forma más común de recolectar datos de sitios web.

## Instalación

### Opción 1: HTML Snippet
Ver [HTML Snippet](javascript-sdk/html-snippet.md)

### Opción 2: NPM
```bash
npm install @jitsu/sdk-js
```

```javascript
import { jitsuClient } from '@jitsu/sdk-js';

const jitsu = jitsuClient({
  key: "js.TU_KEY.AQUI",
  tracking_host: "https://tracking.midas.com"
});
```

## Uso Básico

```javascript
// Track evento
jitsu.track('Product Viewed', {
  product_id: 'PROD-123',
  price: 99.99
});

// Identificar usuario
jitsu.id({
  id: 'user_123',
  email: '[email protected]'
});
```

## Guías Específicas
- [React](javascript-sdk/react.md)
- [Next.js](javascript-sdk/nextjs.md)
- [Configuración](javascript-sdk/configuracion.md)
