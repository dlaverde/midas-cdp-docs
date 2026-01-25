# Marketing & Analytics Tools

Integración con herramientas de marketing y analytics.

## Google Analytics 4

```yaml
destinations:
  ga4:
    type: google_analytics_4
    data:
      measurement_id: "G-XXXXXXXXXX"
      api_secret: "${GA4_API_SECRET}"
```

## Facebook Pixel

```yaml
destinations:
  facebook:
    type: facebook_pixel
    data:
      pixel_id: "123456789"
      access_token: "${FACEBOOK_TOKEN}"
```

## Mixpanel

```yaml
destinations:
  mixpanel:
    type: mixpanel
    data:
      token: "your_mixpanel_token"
```

## Amplitude

```yaml
destinations:
  amplitude:
    type: amplitude
    data:
      api_key: "${AMPLITUDE_API_KEY}"
```

## Próximos Pasos
- [CRM & Sales](crm-sales.md)
- [Webhooks](webhooks.md)
