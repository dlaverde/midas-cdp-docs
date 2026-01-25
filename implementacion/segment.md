# Compatibilidad con Segment

El CDP de Midas es 100% compatible con la API de Segment.

## Migración desde Segment

### Opción 1: Cambio de Endpoint

```javascript
analytics.load("TU_WRITE_KEY_MIDAS", {
  integrations: {
    "Segment.io": {
      apiHost: "tracking.midas.com/api/v1/segment"
    }
  }
});
```

### Opción 2: SDK de Segment

```javascript
const Analytics = require('analytics-node');

const analytics = new Analytics('TU_SERVER_SECRET_MIDAS', {
  host: 'https://tracking.midas.com/api/v1/segment'
});
```

## Métodos Compatibles

Todos los métodos de Segment están soportados:

```javascript
analytics.track('Event Name', {...});
analytics.identify('user_id', {...});
analytics.page('Category', 'Page Name', {...});
analytics.group('company_id', {...});
analytics.alias('new_user_id');
```

## Próximos Pasos
- [Node.js Server-Side](nodejs-server-side.md)
- [JavaScript SDK](javascript-sdk.md)
