# Documentación CDP de Midas - GitBook

Esta carpeta contiene la documentación completa del CDP de Midas organizada para GitBook con navegación multi-página.

## Estructura

```
gitbook-docs/
├── README.md                    # Página principal
├── SUMMARY.md                   # Tabla de contenidos / Navegación
├── conceptos/                   # Conceptos fundamentales
│   ├── composable-cdp.md
│   ├── arquitectura.md
│   └── eventos-propiedades.md
├── comenzando/                  # Guías de inicio
│   ├── instalacion.md
│   └── primeros-pasos.md
├── implementacion/              # Guías de implementación
│   ├── javascript-sdk/
│   │   ├── html-snippet.md
│   │   ├── react.md
│   │   ├── nextjs.md
│   │   └── configuracion.md
│   ├── server-to-server/
│   │   ├── python.md
│   │   ├── nodejs.md
│   │   ├── php.md
│   │   ├── ruby.md
│   │   └── go.md
│   ├── google-tag-manager.md
│   ├── segment.md
│   └── nodejs-server-side.md
├── casos-uso/                   # Casos de uso por industria
│   ├── ecommerce.md
│   ├── saas-b2b.md
│   ├── content-media.md
│   ├── mobile-apps.md
│   └── marketing-attribution.md
├── destinos/                    # Configuración de destinos
│   ├── data-warehouses/
│   │   ├── snowflake.md
│   │   ├── bigquery.md
│   │   ├── redshift.md
│   │   ├── clickhouse.md
│   │   └── postgresql.md
│   ├── marketing-analytics.md
│   ├── crm-sales.md
│   └── webhooks.md
├── funciones/                   # Funciones y transformaciones
│   ├── introduccion.md
│   ├── ejemplos/
│   │   ├── filtrado.md
│   │   ├── enriquecimiento.md
│   │   ├── normalizacion.md
│   │   ├── deduplicacion.md
│   │   ├── notificaciones.md
│   │   └── pii-masking.md
│   ├── npm-packages.md
│   └── key-value-store.md
├── mejores-practicas/           # Best practices
│   ├── convenciones-nombres.md
│   ├── taxonomia-eventos.md
│   ├── identificacion-usuarios.md
│   ├── performance.md
│   ├── privacy-compliance.md
│   ├── testing.md
│   └── monitoring.md
└── recursos/                    # Recursos adicionales
    ├── soporte.md
    ├── faq.md
    └── glosario.md
```

## Cómo Usar con GitBook

### Opción 1: GitBook Cloud (Recomendado)

1. Ve a [GitBook.com](https://www.gitbook.com/) y crea una cuenta
2. Crea un nuevo espacio (Space)
3. Selecciona "Import" → "GitHub" o "Upload files"
4. Sube el contenido de la carpeta `gitbook-docs`
5. GitBook detectará automáticamente el `SUMMARY.md` y creará la navegación

### Opción 2: GitBook CLI (Local)

```bash
# Instalar GitBook CLI
npm install -g gitbook-cli

# Ir al directorio
cd gitbook-docs

# Instalar dependencias
gitbook install

# Servir localmente
gitbook serve
# Visita http://localhost:4000

# Generar sitio estático
gitbook build
# Los archivos HTML estarán en _book/
```

### Opción 3: GitHub Pages

1. Sube el contenido a un repositorio de GitHub
2. GitBook puede sincronizarse automáticamente con GitHub
3. O usa GitHub Pages con Jekyll/Hugo para renderizar

## Características

✅ **Navegación Multi-página**: 55 páginas organizadas en 7 secciones principales
✅ **Búsqueda**: GitBook incluye búsqueda full-text
✅ **Sin Mencionar Jitsu**: Todo el contenido se refiere al "CDP de Midas"
✅ **Ejemplos de Código**: Múltiples lenguajes (JS, Python, PHP, Ruby, Go, Node.js)
✅ **Casos de Uso**: E-commerce, SaaS, Content, Mobile, Marketing
✅ **Composable CDP**: Explicación completa de arquitectura composable

## Archivos Clave

- **SUMMARY.md**: Define la estructura de navegación del sitio
- **README.md**: Página de inicio
- Todos los archivos .md son páginas individuales navegables

## Personalización

Para personalizar la documentación:

1. Edita los archivos `.md` según necesites
2. Actualiza `SUMMARY.md` si agregas/eliminas páginas
3. Las rutas en `SUMMARY.md` deben coincidir con la estructura de archivos

## Formato GitBook

La documentación usa características de GitBook:

- **Bloques de código** con syntax highlighting
- **Tablas** Markdown estándar
- **Links internos** relativos entre páginas
- **Emojis** para mejor UX (✅, 📚, 💬, etc.)

## Contenido Incluido

### Conceptos
- Qué es un Composable CDP
- Arquitectura del CDP de Midas
- Eventos y Propiedades

### Implementación
- JavaScript SDK (HTML, React, Next.js)
- Google Tag Manager
- Server-to-Server (5 lenguajes)
- Compatibilidad con Segment
- Node.js Server-Side

### Casos de Uso
- E-commerce y Retail
- SaaS y B2B
- Content y Media
- Mobile Apps
- Marketing Attribution

### Destinos
- Data Warehouses (5 tipos)
- Marketing & Analytics
- CRM & Sales
- Webhooks

### Funciones
- Introducción a Funciones
- 6 ejemplos de transformaciones
- NPM Packages
- Key-Value Store

### Mejores Prácticas
- Convenciones de nombres
- Taxonomía de eventos
- Identificación de usuarios
- Performance
- Privacy y Compliance
- Testing
- Monitoring

## Soporte

Para preguntas sobre esta documentación:
- GitHub: https://github.com/jitsucom/jitsu
- Email: [email protected]

---

**Total de páginas**: 55 archivos Markdown
**Idioma**: Español
**Formato**: Compatible con GitBook
