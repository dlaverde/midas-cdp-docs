# ClickHouse

Configuración de ClickHouse como destino.

## Configuración YAML

```yaml
destinations:
  clickhouse_prod:
    type: clickhouse
    mode: stream
    data:
      # Credenciales específicas de ClickHouse
      host: "clickhouse-1.example.com:8123"
      # ... más configuración
```

## Configuración vía UI

1. Ve a **Destinations** → **Add Destination**
2. Selecciona **ClickHouse**
3. Ingresa credenciales
4. Test Connection
5. Save

## Próximos Pasos
- [Data Warehouses](../data-warehouses.md)
- [Marketing & Analytics](../marketing-analytics.md)
