# E-commerce y Retail

Tracking completo del customer journey en e-commerce.

## Customer Journey

```javascript
// 1. Usuario llega al sitio
analytics.page('Home');

// 2. Busca productos
analytics.track('Product Search', {
  query: 'zapatillas running',
  results_count: 45
});

// 3. Ve un producto
analytics.track('Product Viewed', {
  product_id: 'SHOE-123',
  product_name: 'Nike Air Zoom',
  price: 129.99,
  category: 'Running Shoes'
});

// 4. Agrega al carrito
analytics.track('Product Added', {
  product_id: 'SHOE-123',
  quantity: 1,
  cart_total: 129.99
});

// 5. Checkout
analytics.track('Checkout Started', {
  order_id: 'ORD-789',
  cart_total: 129.99
});

// 6. Compra
analytics.track('Order Completed', {
  order_id: 'ORD-789',
  total: 129.99,
  revenue: 129.99,
  products: [{
    product_id: 'SHOE-123',
    price: 129.99,
    quantity: 1
  }]
});
```

## Abandoned Cart

```javascript
analytics.track('Product Added', {
  cart_id: 'cart_123',
  product_id: 'PROD-456',
  email: '[email protected]'
});
```

Después de 1 hora sin compra, activa workflow de recuperación.

## Próximos Pasos
- [SaaS y B2B](saas-b2b.md)
- [Funciones de Transformación](../funciones/introduccion.md)
