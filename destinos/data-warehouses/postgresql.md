# PostgreSQL

Configuración de PostgreSQL como destino.

## Configuración YAML

```yaml
destinations:
  postgresql_prod:
    type: postgresql
    mode: stream
    data:
      # Credenciales específicas de PostgreSQL
      host: "postgres.example.com"
      # ... más configuración
```

## Configuración vía UI

1. Ve a **Destinations** → **Add Destination**
2. Selecciona **PostgreSQL**
3. Ingresa credenciales
4. Test Connection
5. Save

## Próximos Pasos
- [Data Warehouses](../data-warehouses.md)
- [Marketing & Analytics](../marketing-analytics.md)
