# SaaS y B2B

Tracking para aplicaciones SaaS y modelos B2B.

## Onboarding Tracking

```javascript
// Signup
analytics.identify('user_123', {
  email: '[email protected]',
  company: 'ACME Corp',
  signup_date: new Date().toISOString()
});

analytics.track('Account Created', {
  plan: 'trial',
  trial_days: 14
});

// Completar perfil
analytics.track('Profile Completed', {
  completion_percentage: 100
});

// Primer proyecto
analytics.track('Project Created', {
  project_name: 'My First Project',
  days_since_signup: 0
});

// Feature adoption
analytics.track('Feature Used', {
  feature_name: 'Dashboard',
  first_use: true
});
```

## Product Analytics

```javascript
// Track features
analytics.track('Feature Used', {
  feature: 'export_data',
  format: 'csv',
  rows_exported: 1000
});

// Track errors
analytics.track('Error Occurred', {
  error_type: 'validation_error',
  page: '/settings/profile'
});
```

## Conversion Tracking

```javascript
// Trial to Paid
analytics.track('Trial Converted', {
  from_plan: 'trial',
  to_plan: 'professional',
  days_in_trial: 7,
  revenue: 99.99
});

// Upsell
analytics.track('Plan Upgraded', {
  from_plan: 'basic',
  to_plan: 'enterprise',
  upgrade_revenue: 500
});
```

## Próximos Pasos
- [Content y Media](content-media.md)
- [Marketing Attribution](marketing-attribution.md)
