# Instalación

## Credenciales

Antes de comenzar, necesitas obtener de tu account manager:

| Credencial | Uso | Ejemplo |
|------------|-----|---------|
| **Write Key** | Cliente (navegador) | `js.abc123def456.xyz` |
| **Server Secret** | Backend | `s2s.secret.key.here` |
| **Tracking Host** | URL del CDP | `https://cdp.companydomain.m1das.app/p.js` |

⚠️ **Importante**: Nunca expongas tu Server Secret en el navegador.

## Instalación para Web

### Opción 1: Script Tag (Más Simple)

Agrega este código antes del cierre de `</head>`:

```html
<script 
  src="https://cdp.companydomain.m1das.app/p.js" 
  data-write-key="TU_WRITE_KEY"
  defer>
</script>
```

Esto carga el SDK automáticamente y lo hace disponible como `window.jitsu`.

### Otros Lenguajes

Para Python, Ruby, PHP, etc., usa la [HTTP API](../tracking/backend/http-api.md).

## Verificar Instalación

Después de instalar, envía un evento de prueba:

```javascript
jitsu.track('test_event', {
  message: 'Hello from CDP de Midas!'
});
```

Verifica en tu data warehouse que el evento llegó correctamente.

## Próximos Pasos

- [Conceptos Básicos](conceptos.md)
- [Tu Primer Evento](primer-evento.md)
- [JavaScript SDK](../tracking/web/javascript.md)
