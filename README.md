# Documentación del CDP de Midas

Bienvenido a la documentación oficial del CDP de Midas, una plataforma de datos de clientes (Customer Data Platform) de última generación que utiliza una arquitectura composable para ofrecer máxima flexibilidad, control y eficiencia en la gestión de datos de clientes.

## ¿Qué es el CDP de Midas?

El CDP de Midas es una solución composable que te permite:

- **Recolectar** eventos de múltiples fuentes (web, móvil, backend, third-party)
- **Almacenar** datos en tu propio data warehouse (zero-copy architecture)
- **Transformar** y enriquecer datos en tiempo real
- **Activar** datos hacia herramientas de marketing y analytics

### Características Principales

- ✅ **Composable por diseño**: Integración nativa con tu data warehouse existente
- ✅ **Zero-copy architecture**: Los datos permanecen en tu infraestructura
- ✅ **Open-source**: 100% código abierto bajo licencia MIT
- ✅ **Auto-hospedable**: Despliega en tu propia infraestructura o usa la versión en la nube
- ✅ **Compatible con Segment**: Migración sin interrupciones desde Segment
- ✅ **Múltiples métodos de recolección**: JavaScript, HTTP API, SDKs nativos, y más
- ✅ **300+ conectores**: Integración con las principales plataformas de datos

## Inicio Rápido

### 1. Crear una Cuenta

Regístrate en el portal de Midas y obtén tu **Write Key** (Client Secret).

### 2. Configurar Destino

Conecta tu data warehouse (Snowflake, BigQuery, Redshift, etc.).

### 3. Instalar SDK

```html
<script>
  !function(){var analytics=window.analytics=window.analytics||[];if(!analytics.initialize)if(analytics.invoked)window.console&&console.error&&console.error("Snippet included twice.");else{analytics.invoked=!0;analytics.methods=["trackSubmit","trackClick","trackLink","trackForm","pageview","identify","reset","group","track","ready","alias","debug","page","once","off","on"];analytics.factory=function(e){return function(){var t=Array.prototype.slice.call(arguments);t.unshift(e);analytics.push(t);return analytics}};for(var e=0;e<analytics.methods.length;e++){var key=analytics.methods[e];analytics[key]=analytics.factory(key)}analytics.load=function(key,e){var t=document.createElement("script");t.type="text/javascript";t.async=!0;t.src="https://cdn.midas.com/analytics.min.js";var n=document.getElementsByTagName("script")[0];n.parentNode.insertBefore(t,n);analytics._loadOptions=e};analytics._writeKey="TU_CLIENT_SECRET_AQUI";;analytics.SNIPPET_VERSION="4.15.3";
  analytics.load("TU_CLIENT_SECRET_AQUI");
  analytics.page();
  }}();
</script>
```

### 4. Enviar tu Primer Evento

```javascript
analytics.track('Button Clicked', {
  button_name: 'Get Started',
  location: 'homepage'
});
```

## Explorar la Documentación

Utiliza el menú de navegación de la izquierda para explorar:

- **Conceptos**: Aprende sobre Composable CDPs y arquitectura
- **Guías de Implementación**: Implementa tracking en diferentes plataformas
- **Casos de Uso**: Ejemplos prácticos por industria
- **Referencia**: Documentación técnica completa
- **Mejores Prácticas**: Aprende a optimizar tu implementación

## Necesitas Ayuda?

- 📚 **Documentación**: Estás aquí
- 💬 **Community**: https://community.midas.com
- 🐙 **GitHub**: https://github.com/jitsucom/jitsu
- 📧 **Email**: [email protected]

---

**Plan Gratuito**: Comienza con hasta 200,000 eventos/mes con instancia ClickHouse incluida.
