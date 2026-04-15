# Data Warehouses

El CDP de Midas envía todos tus eventos a tu data warehouse.

## Warehouses Soportados

- ✅ Snowflake
- ✅ Google BigQuery
- ✅ Amazon Redshift  
- ✅ PostgreSQL
- ✅ ClickHouse

## Configuración

Tu account manager configurará la conexión a tu warehouse. Necesitarás proporcionar:

### Snowflake
- Account URL
- Database y Schema
- Username y Password
- Warehouse name

### BigQuery
- Project ID
- Dataset
- Service Account JSON

### Redshift
- Host y Port
- Database y Schema
- Username y Password

### PostgreSQL
- Host y Port
- Database y Schema
- Username y Password

## Esquema de Datos

Los eventos se almacenan en una tabla `events`:

```sql
CREATE TABLE events (
  id UUID PRIMARY KEY,
  event VARCHAR,
  user_id VARCHAR,
  anonymous_id VARCHAR,
  timestamp TIMESTAMP,
  properties JSON,
  context JSON
);
```

## Queries de Ejemplo

### Eventos del día
```sql
SELECT event, COUNT(*) as count
FROM events
WHERE DATE(timestamp) = CURRENT_DATE
GROUP BY event;
```

### Eventos por usuario
```sql
SELECT user_id, COUNT(*) as event_count
FROM events
WHERE user_id IS NOT NULL
GROUP BY user_id
ORDER BY event_count DESC
LIMIT 10;
```

## Próximos Pasos

- [Configuración](configuracion.md)
- [Referencia de API](../referencia/api.md)
