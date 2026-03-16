# Tracking Web

Guías para implementar tracking en aplicaciones web.

## Métodos Disponibles

| Método | Mejor Para | Dificultad |
|--------|-----------|------------|
| [JavaScript](javascript.md) | Sitios estáticos, WordPress | ⭐ Fácil |

## Inicio Rápido

```html
<script 
  src="https://cdp.companydomain.m1das.app/p.js" 
  data-write-key="TU_WRITE_KEY"
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

## Próximos Pasos

- [JavaScript SDK](javascript.md) - Guía completa
