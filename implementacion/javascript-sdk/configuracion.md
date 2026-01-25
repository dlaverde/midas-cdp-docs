# Configuración del SDK

Parámetros disponibles para `jitsuClient()`.

## Parámetros Básicos

```javascript
const jitsu = jitsuClient({
  key: "js.your.key.here",           // REQUERIDO
  tracking_host: "https://...",      // REQUERIDO
  
  log_level: 'ERROR',                // DEBUG, INFO, WARN, ERROR
  cookie_name: '__midas_id',
  cookie_domain: 'midominio.com',
  capture_3rd_party_cookies: false,
  randomize_url: true,               // Anti-adblocker
});
```

## Interceptors

```javascript
const jitsu = jitsuClient({
  key: "...",
  ga_hook: true,      // Interceptar Google Analytics
  segment_hook: true, // Interceptar Segment
});
```

## Privacy

```javascript
const jitsu = jitsuClient({
  key: "...",
  privacy_policy: 'strict', // 'strict' o 'comply'
});
```

## Próximos Pasos
- [Google Tag Manager](../google-tag-manager.md)
- [Mejores Prácticas](../../mejores-practicas/convenciones-nombres.md)
