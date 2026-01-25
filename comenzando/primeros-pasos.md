# Primeros Pasos

Guía rápida para enviar tu primer evento.

## 1. Instalar SDK

```html
<script>
  !function(){var analytics=window.analytics=window.analytics||[];
  /* ... snippet completo ... */
  analytics.load("TU_CLIENT_SECRET");
  analytics.page();
  }}();
</script>
```

## 2. Identificar Usuario

```javascript
analytics.identify('user_123', {
  email: '[email protected]',
  name: 'Juan Pérez'
});
```

## 3. Track Evento

```javascript
analytics.track('Button Clicked', {
  button_name: 'Get Started'
});
```

## 4. Verificar en Live Events

Ve a la UI y verifica que los eventos aparezcan.

## Próximos Pasos
- [JavaScript SDK Completo](../implementacion/javascript-sdk.md)
- [Casos de Uso](../casos-uso/ecommerce.md)
