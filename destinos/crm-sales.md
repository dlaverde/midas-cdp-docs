# CRM & Sales Tools

Integración con CRMs y herramientas de ventas.

## Salesforce

```yaml
destinations:
  salesforce:
    type: salesforce
    data:
      username: "[email protected]"
      password: "${SALESFORCE_PASSWORD}"
      security_token: "${SALESFORCE_TOKEN}"
```

## HubSpot

```yaml
destinations:
  hubspot:
    type: hubspot
    data:
      api_key: "${HUBSPOT_API_KEY}"
```

## Próximos Pasos
- [Webhooks](webhooks.md)
- [Funciones](../funciones/introduccion.md)
