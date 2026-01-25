# Webhooks

Envía eventos a cualquier servicio custom vía webhooks.

## Configuración

```yaml
destinations:
  custom_webhook:
    type: webhook
    data:
      url: "https://api.example.com/events"
      method: "POST"
      headers:
        Authorization: "Bearer ${API_TOKEN}"
        Content-Type: "application/json"
```

## Formato de Payload

Los eventos se envían en el formato estándar del CDP.

## Retry Logic

- Reintentos automáticos en caso de fallo
- Exponential backoff
- Dead letter queue para eventos no entregables

## Próximos Pasos
- [Data Warehouses](data-warehouses.md)
- [Funciones](../funciones/introduccion.md)
