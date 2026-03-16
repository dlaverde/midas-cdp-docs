# Tracking Web

Guías para implementar tracking en aplicaciones web.

## Métodos Disponibles

| Método | Mejor Para | Dificultad |
|--------|-----------|------------|
| [JavaScript](javascript.md) | Sitios estáticos, WordPress | ⭐ Fácil |
| [React](react.md) | Apps React | ⭐⭐ Media |
| [Next.js](nextjs.md) | Apps Next.js | ⭐⭐ Media |
| [GTM](gtm.md) | Sin acceso a código | ⭐ Fácil |

## Inicio Rápido

```html
<script 
  src="https://cdp.companydomain.m1das.app/p.js" 
  data-write-key="TU_WRITE_KEY"
  data-tracking-host="https://cdp.companydomain.m1das.app/p.js"
  defer>
</script>
```

Luego trackea eventos:

```javascript
jitsu.track('event_name', { property: 'value' });
```

## Elección del Método

**¿Tienes acceso al código?**
- Sí → Usa JavaScript SDK
- No → Usa Google Tag Manager

**¿Usas un framework?**
- React → Usa SDK de React
- Next.js → Usa SDK de Next.js
- Otro → Usa JavaScript vanilla

## Próximos Pasos

- [JavaScript SDK](javascript.md) - Guía completa
- [React Integration](react.md) - Para apps React
