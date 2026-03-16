# CDP de Midas - Documentación

Bienvenido a la documentación oficial del CDP de Midas, tu plataforma de datos de clientes de próxima generación.

## ¿Qué es el CDP de Midas?

El CDP de Midas es una plataforma composable de datos de clientes que te permite:

- **Capturar** eventos de usuarios en tiempo real desde web, móvil y backend
- **Almacenar** toda tu data en tu propio data warehouse
- **Activar** datos hacia tus herramientas de marketing y analytics
- **Transformar** datos con funciones JavaScript personalizables

## Características Principales

✅ **Sin vendor lock-in** - Tus datos viven en TU warehouse  
✅ **Open-source** - Basado en tecnología MIT  
✅ **Compatible con Segment** - Migración sin fricciones  
✅ **Funciones JavaScript** - Transforma datos en tiempo real  
✅ **Multiple SDKs** - Web, Mobile, Backend

## Inicio Rápido

### 1. Obtén tus credenciales

Contacta a tu account manager para obtener:
- **Write Key**: Para enviar eventos desde el navegador
- **Server Secret**: Para enviar eventos desde tu backend
- **Tracking Host**: URL de tu instancia del CDP

### 2. Instala el SDK

**Para sitios web:**

```html
<script src="https://cdp.companydomain.m1das.app/p.js" 
        data-write-key="TU_WRITE_KEY" 
        defer></script>
```

### 3. Envía tu primer evento

```javascript
jitsu.track('button_clicked', {
  button_name: 'Get Started',
  page: '/landing'
});
```

## Estructura de la Documentación

- **[Comenzando](comenzando/instalacion.md)** - Configuración inicial
- **[Tracking](tracking/web/javascript.md)** - Guías de implementación
- **[Destinos](destinos/warehouses.md)** - Configurar data warehouses
- **[Casos de Uso](casos-uso/ecommerce.md)** - Ejemplos prácticos
- **[Referencia](referencia/api.md)** - API completa

## Soporte

¿Necesitas ayuda?
- 📧 Email: [email protected]
- 💬 Slack: [Tu canal de Slack]
- 📚 Documentación: Esta guía

---

**Última actualización**: Enero 2026
