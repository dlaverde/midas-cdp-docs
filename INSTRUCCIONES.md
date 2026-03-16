# CDP de Midas - Documentación para Clientes

Esta es la documentación actualizada y simplificada del CDP de Midas para clientes.

## Cambios Principales vs Versión Anterior

✅ **Actualizada** - Basada en la versión moderna (no Classic)
✅ **Simplificada** - Solo lo esencial para clientes
✅ **Clara** - Sin confusiones sobre configuración classic
✅ **Práctica** - Ejemplos reales y casos de uso

## Estructura

```
gitbook-docs-v2/
├── README.md                    # Inicio
├── SUMMARY.md                   # Navegación
├── comenzando/                  # Primeros pasos
│   ├── instalacion.md
│   ├── conceptos.md
│   └── primer-evento.md
├── tracking/                    # Guías de implementación
│   ├── web/
│   │   ├── javascript.md
│   ├── mobile/
│   └── backend/
│       └── http-api.md
├── destinos/                    # Data warehouses
│   ├── warehouses.md
│   └── configuracion.md
├── casos-uso/                   # Ejemplos prácticos
│   └── ecommerce.md
├── referencia/                  # Documentación técnica
│   ├── api.md
│   └── eventos.md
└── recursos/                    # Ayuda adicional
    ├── faq.md
    └── mejores-practicas.md
```

## Cómo Importar en GitBook

### Opción 1: GitHub (Recomendado)

1. Sube esta carpeta a GitHub
2. En GitBook → Integrations → GitHub
3. Conecta el repositorio
4. GitBook sincronizará automáticamente

### Opción 2: Upload Manual

1. En GitBook → Import
2. Selecciona todos los archivos .md
3. GitBook detectará el SUMMARY.md automáticamente

## Diferencias con Documentación Anterior

| Aspecto | Anterior | Nueva |
|---------|----------|-------|
| Base | Jitsu Classic | Jitsu Moderno |
| Enfoque | Técnico/Completo | Cliente/Práctico |
| Configuración | Classic (deprecado) | Actual |
| Ejemplos | Limitados | Abundantes |
| Claridad | Confusa | Directa |

## Lo que Incluye

- ✅ Instalación paso a paso
- ✅ Conceptos básicos explicados
- ✅ HTTP API para cualquier lenguaje
- ✅ Casos de uso de E-commerce
- ✅ FAQ completo
- ✅ Mejores prácticas

## Lo que NO Incluye

- ❌ Configuración de infraestructura (manejado por Midas)
- ❌ Detalles internos de implementación
- ❌ Features avanzados no relevantes para clientes

---

**Versión**: 2.0  
**Fecha**: Enero 2026
