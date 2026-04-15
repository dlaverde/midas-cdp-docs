# Tu Primer Evento

Esta guía te llevará paso a paso para enviar tu primer evento al CDP de Midas.

## Paso 1: Instalar SDK

Si aún no lo has hecho, agrega el SDK a tu sitio:

```html
<script 
  src="https://cdp.companydomain.m1das.app/p.js" 
  data-write-key="TU_WRITE_KEY"
  defer>
</script>
```

## Paso 2: Identificar al Usuario

Cuando un usuario inicia sesión o se registra:

```javascript
jitsu.identify({
  id: 'user_123',
  email: '[email protected]',
  name: 'Ana Martínez'
});
```

## Paso 3: Trackear un Evento

Trackea una acción del usuario:

```javascript
jitsu.track('button_clicked', {
  button_name: 'Comenzar Prueba Gratuita',
  button_location: 'hero_section',
  page: '/pricing'
});
```

## Paso 4: Track Automático de Pageviews

El SDK trackea pageviews automáticamente cuando se carga. Para SPAs:

```javascript
// Al cambiar de ruta
jitsu.page({
  name: 'Dashboard',
  category: 'App'
});
```

## Ejemplo Completo: E-commerce

```html
<!DOCTYPE html>
<html>
<head>
  <!-- CDP de Midas SDK -->
  <script 
    src="https://cdp.companydomain.m1das.app/p.js" 
    data-write-key="js.abc123.xyz"
    defer>
  </script>
</head>
<body>
  <button id="add-to-cart">Agregar al Carrito</button>
  
  <script>
    // Identificar usuario (si está logueado)
    jitsu.identify({
      id: 'user_456',
      email: '[email protected]'
    });
    
    // Trackear click en botón
    document.getElementById('add-to-cart')
      .addEventListener('click', function() {
        jitsu.track('product_added_to_cart', {
          product_id: 'PROD-789',
          product_name: 'Camiseta Premium',
          price: 29.99,
          quantity: 1
        });
      });
  </script>
</body>
</html>
```

## Siguiente Paso

Ahora que tienes eventos fluyendo, explora:

- [JavaScript SDK Completo](../tracking/web/javascript.md)
- [Casos de Uso de E-commerce](../casos-uso/ecommerce.md)
- [Estructura de Eventos](../referencia/eventos.md)
