# Conceptos Básicos

## Eventos

Un **evento** es cualquier acción que un usuario realiza. Ejemplos:
- Visitó una página
- Hizo clic en un botón
- Completó un formulario
- Realizó una compra

### Anatomía de un Evento

```javascript
{
  "event": "product_viewed",
  "userId": "user_123",
  "timestamp": "2026-01-24T10:30:00.000Z",
  "properties": {
    "product_id": "PROD-456",
    "product_name": "Zapatos Deportivos",
    "price": 89.99,
    "category": "Calzado"
  },
  "context": {
    "page": {
      "url": "https://tienda.com/productos/zapatos-deportivos"
    },
    "userAgent": "Mozilla/5.0...",
    "ip": "192.168.1.1"
  }
}
```

## Tipos de Llamadas

### 1. track()
Registra eventos que un usuario realiza:

```javascript
jitsu.track('button_clicked', {
  button_name: 'Agregar al Carrito',
  product_id: 'PROD-456'
});
```

### 2. identify()
Asocia un usuario con sus atributos:

```javascript
jitsu.identify({
  id: 'user_123',
  email: '[email protected]',
  name: 'María García',
  plan: 'premium'
});
```

### 3. page()
Registra vistas de página:

```javascript
jitsu.page({
  name: 'Página de Producto',
  category: 'E-commerce'
});
```

## Properties vs Traits

**Properties** = Información sobre el EVENTO  
**Traits** = Información sobre el USUARIO

```javascript
// Properties (del evento)
jitsu.track('purchase_completed', {
  order_id: 'ORD-789',      // qué se compró
  total: 99.99,             // cuánto costó
  currency: 'USD'           // en qué moneda
});

// Traits (del usuario)
jitsu.identify({
  id: 'user_123',           // quién es
  email: '[email protected]', // cómo contactarlo
  plan: 'premium'           // qué tipo de cliente
});
```

## Context (Automático)

El SDK captura automáticamente:
- URL de la página
- User Agent
- IP del usuario
- Parámetros UTM
- Timestamp
- Device info

No necesitas enviar esta información manualmente.

## Data Warehouse

Todos tus eventos se almacenan en tu propio data warehouse:
- Snowflake
- BigQuery
- Redshift
- PostgreSQL
- ClickHouse

**Ventaja**: Tienes control total de tus datos.

## Próximos Pasos

- [Tu Primer Evento](primer-evento.md)
- [JavaScript SDK](../tracking/web/javascript.md)
