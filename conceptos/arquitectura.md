# Arquitectura del CDP de Midas

El CDP de Midas utiliza una arquitectura moderna y escalable diseñada para procesar millones de eventos en tiempo real.

## Flujo de Datos

```
[Fuentes] → [CDP Midas] → [Data Warehouse] → [Activación]
```

## Componentes Técnicos

### Motor de Ingestión
- Procesamiento en tiempo real
- Cola persistente
- Auto-retry en fallos
- Batching inteligente

### Identity Graph
- Unificación incremental en tiempo real
- Resolución cross-device
- Merge basado en reglas

### Funciones JavaScript
- Runtime JavaScript para transformaciones
- Acceso a NPM packages
- Key-value storage integrado

## Garantías

- **At-Least-Once Delivery**
- **Orden de Eventos** preservado
- **Retry Logic** con exponential backoff

## Seguridad

- TLS 1.3 en tránsito
- Encriptación en reposo
- GDPR, SOC 2, ISO 27001 compliant

## Próximos Pasos

- [Eventos y Propiedades](eventos-propiedades.md)
- [Instalación](../comenzando/instalacion.md)
