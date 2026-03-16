# E-commerce

Guía completa de tracking para tiendas online.

## Customer Journey

### 1. Usuario llega al sitio

```javascript
// Pageview automático
```

### 2. Busca productos

```javascript
jitsu.track('products_searched', {
  query: 'zapatos running',
  results_count: 24
});
```

### 3. Ve un producto

```javascript
jitsu.track('product_viewed', {
  product_id: 'PROD-123',
  product_name: 'Nike Air Zoom',
  category: 'Zapatos/Running',
  price: 129.99,
  currency: 'USD'
});
```

### 4. Agrega al carrito

```javascript
jitsu.track('product_added', {
  product_id: 'PROD-123',
  product_name: 'Nike Air Zoom',
  price: 129.99,
  quantity: 1,
  cart_total: 129.99
});
```

### 5. Inicia checkout

```javascript
jitsu.track('checkout_started', {
  cart_id: 'cart_789',
  value: 129.99,
  currency: 'USD',
  products: [{
    product_id: 'PROD-123',
    quantity: 1,
    price: 129.99
  }]
});
```

### 6. Completa compra

```javascript
jitsu.track('order_completed', {
  order_id: 'ORD-456',
  revenue: 129.99,
  tax: 10.40,
  shipping: 0,
  currency: 'USD',
  products: [{
    product_id: 'PROD-123',
    name: 'Nike Air Zoom',
    price: 129.99,
    quantity: 1
  }]
});
```

## Implementación Completa

```javascript
// Identificar usuario
jitsu.identify({
  id: user.id,
  email: user.email,
  name: user.name
});

// Producto visto
document.addEventListener('DOMContentLoaded', () => {
  jitsu.track('product_viewed', {
    product_id: window.productData.id,
    product_name: window.productData.name,
    price: window.productData.price
  });
});

// Agregar al carrito
document.getElementById('add-to-cart').addEventListener('click', () => {
  jitsu.track('product_added', {
    product_id: window.productData.id,
    product_name: window.productData.name,
    price: window.productData.price,
    quantity: 1
  });
});

// Checkout completado
if (window.location.pathname === '/gracias') {
  jitsu.track('order_completed', {
    order_id: window.orderData.id,
    revenue: window.orderData.total,
    products: window.orderData.items
  });
}
```

## Próximos Pasos

- [SaaS](saas.md) - Tracking para SaaS
- [Referencia de Eventos](../referencia/eventos.md)
