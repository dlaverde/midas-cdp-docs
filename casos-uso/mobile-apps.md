# Mobile Apps

Tracking para aplicaciones móviles nativas.

## App Lifecycle

```javascript
// App opened
analytics.track('Application Opened', {
  version: '2.5.0',
  build: '125',
  from_background: false
});

// Screen viewed
analytics.screen('Product List', {
  category: 'Shopping',
  items_count: 20
});

// App backgrounded
analytics.track('Application Backgrounded', {
  session_length_seconds: 180
});
```

## In-App Purchases

```javascript
analytics.track('Product Purchased', {
  product_id: 'premium_monthly',
  product_name: 'Premium Subscription',
  price: 9.99,
  currency: 'USD',
  payment_method: 'apple_pay'
});
```

## Próximos Pasos
- [Marketing Attribution](marketing-attribution.md)
- [E-commerce](ecommerce.md)
