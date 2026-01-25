# Instalación y Configuración

Esta guía te ayudará a configurar el CDP de Midas en minutos.

## Requisitos Previos

Necesitas un data warehouse:
- Snowflake, BigQuery, Redshift, ClickHouse, o PostgreSQL

## Opción 1: Cloud (Recomendado)

### Paso 1: Crear Cuenta
1. Visita https://app.midas.com/signup
2. Verifica tu email

### Paso 2: Obtener Write Key
```
Client Secret: js.abc123def456.xyz789
Server Secret: s2s.secret.key.here
```

### Paso 3: Configurar Destino
Conect tu data warehouse desde la UI.

## Opción 2: Auto-hospedaje

```bash
git clone --depth 1 https://github.com/jitsucom/jitsu
cd jitsu/docker
docker-compose up -d
```

## Próximos Pasos
- [Primeros Pasos](primeros-pasos.md)
- [JavaScript SDK](../implementacion/javascript-sdk.md)
