# PII Masking

Protege información personal sensible.

## Maskear Emails

```javascript
export default async function(event, { log }) {
  function maskEmail(email) {
    const [username, domain] = email.split('@');
    const masked = username.substring(0, 2) + '***';
    return `${masked}@${domain}`;
  }
  
  if (event.traits?.email) {
    log(`Masking email: ${event.traits.email}`);
    event.traits.email_masked = maskEmail(event.traits.email);
    delete event.traits.email;
  }
  
  return event;
}
```

## Maskear Tarjetas de Crédito

```javascript
export default async function(event) {
  if (event.properties?.credit_card) {
    const cc = event.properties.credit_card;
    event.properties.credit_card = `****-****-****-${cc.slice(-4)}`;
  }
  
  return event;
}
```

## Próximos Pasos
- [Enriquecimiento](enriquecimiento.md)
- [Mejores Prácticas de Privacy](../../../mejores-practicas/privacy-compliance.md)
