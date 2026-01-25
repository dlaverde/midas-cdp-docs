# Amazon Redshift

Configuración de Amazon Redshift como destino.

## Configuración YAML

```yaml
destinations:
  redshift_prod:
    type: redshift
    mode: stream
    data:
      # Credenciales específicas de Amazon Redshift
      host: "my-cluster.abc123.us-east-1.redshift.amazonaws.com"
      # ... más configuración
```

## Configuración vía UI

1. Ve a **Destinations** → **Add Destination**
2. Selecciona **Amazon Redshift**
3. Ingresa credenciales
4. Test Connection
5. Save

## Próximos Pasos
- [Data Warehouses](../data-warehouses.md)
- [Marketing & Analytics](../marketing-analytics.md)
