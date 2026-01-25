# Snowflake

Configuración de Snowflake como destino.

## Configuración YAML

```yaml
destinations:
  snowflake_prod:
    type: snowflake
    mode: stream
    data:
      # Credenciales específicas de Snowflake
      host: "xy12345.us-east-1"
      # ... más configuración
```

## Configuración vía UI

1. Ve a **Destinations** → **Add Destination**
2. Selecciona **Snowflake**
3. Ingresa credenciales
4. Test Connection
5. Save

## Próximos Pasos
- [Data Warehouses](../data-warehouses.md)
- [Marketing & Analytics](../marketing-analytics.md)
