# Convenciones de Nombres

Guía de naming para eventos y propiedades.

## Eventos

### Usa "Objeto + Acción"

```javascript
// ✅ Correcto
analytics.track('Email Opened');
analytics.track('Product Viewed');
analytics.track('Checkout Completed');

// ❌ Incorrecto
analytics.track('open_email');
analytics.track('CHECKOUT_COMPLETE');
```

### Title Case Consistente

```javascript
// ✅ Correcto
analytics.track('Button Clicked');
analytics.track('Form Submitted');

// ❌ Incorrecto
analytics.track('button_clicked');
analytics.track('FORM_SUBMIT');
```

## Propiedades

### snake_case

```javascript
// ✅ Correcto
{
  product_id: 'PROD-123',
  product_name: 'Premium Plan',
  order_total: 99.99
}

// ❌ Incorrecto
{
  productId: 'PROD-123',     // camelCase
  'order-total': 99.99       // kebab-case
}
```

### Tipos Consistentes

```javascript
// ✅ Correcto
{
  price: 99.99,              // number
  quantity: 1,               // number
  is_subscriber: true        // boolean
}

// ❌ Incorrecto
{
  price: '99.99',            // string
  quantity: '1'              // string
}
```

## Próximos Pasos
- [Taxonomía de Eventos](taxonomia-eventos.md)
- [Identificación de Usuarios](identificacion-usuarios.md)
