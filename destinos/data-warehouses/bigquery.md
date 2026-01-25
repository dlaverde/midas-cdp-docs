# Google BigQuery

Configuración de Google BigQuery como destino.

## Configuración YAML

```yaml
destinations:
  bigquery_prod:
    type: bigquery
    mode: stream
    data:
      # Credenciales específicas de Google BigQuery
      host: "my-project-123"
      # ... más configuración
```

## Configuración vía UI

1. Ve a **Destinations** → **Add Destination**
2. Selecciona **Google BigQuery**
3. Ingresa credenciales
4. Test Connection
5. Save

## Próximos Pasos
- [Data Warehouses](../data-warehouses.md)
- [Marketing & Analytics](../marketing-analytics.md)
