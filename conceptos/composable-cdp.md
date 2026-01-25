# ¿Qué es un Composable CDP?

Un **Composable CDP** representa la evolución de las plataformas de datos de clientes tradicionales. A diferencia de los CDPs monolíticos que almacenan una copia separada de tus datos, un Composable CDP se construye sobre tu infraestructura de datos existente.

## Componentes de un Composable CDP

### 1. Recolección de Datos (Data Ingestion)

Captura de eventos en tiempo real desde múltiples fuentes:
- Sitios web y aplicaciones móviles
- Backends y APIs
- Plataformas de terceros (CRM, Analytics, Marketing)
- Datos transaccionales y operacionales

### 2. Almacenamiento y Modelado

- **Single Source of Truth**: Tu data warehouse
- **No duplicación de datos**: Zero-copy architecture
- **Modelado flexible**: Define tus propios esquemas
- **Identity Resolution**: Unificación automática de perfiles

### 3. Activación de Datos

- Sincronización en tiempo real con herramientas de marketing
- Reverse ETL para activar datos del warehouse
- Segmentación de audiencias sin código

## CDP Tradicional vs Composable CDP

| Aspecto | CDP Tradicional | Composable CDP |
|---------|----------------|----------------|
| **Almacenamiento** | Copia separada | Tu data warehouse |
| **Costo** | Alto | Bajo (hasta 90% menos) |
| **Flexibilidad** | Limitada | Completa |
| **Time to Value** | 3-6 meses | 1-7 días |
| **Lock-in** | Alto | Bajo |
| **Seguridad** | Servidor del proveedor | Tu infraestructura |

## Próximos Pasos

- [Arquitectura del CDP de Midas](arquitectura.md)
- [Eventos y Propiedades](eventos-propiedades.md)
