# Marketing Attribution

Trackea campañas y atribución de marketing.

## Campaign Tracking

```javascript
// Landing desde ad
analytics.page('Landing Page', {
  utm_source: 'google',
  utm_medium: 'cpc',
  utm_campaign: 'summer_sale',
  utm_term: 'running shoes',
  utm_content: 'ad_variant_a'
});

// Conversión
analytics.track('Form Submitted', {
  form_name: 'contact_sales',
  utm_source: 'google',
  utm_campaign: 'summer_sale'
});
```

## A/B Testing

```javascript
// Asignar variante
analytics.track('Experiment Viewed', {
  experiment_id: 'pricing_page_test',
  variant_id: 'variant_b',
  variant_name: 'Annual First'
});

// Track conversión
analytics.track('Signup Completed', {
  experiment_id: 'pricing_page_test',
  variant_id: 'variant_b'
});
```

## Próximos Pasos
- [E-commerce](ecommerce.md)
- [Mejores Prácticas](../mejores-practicas/convenciones-nombres.md)
