# Privacy y Compliance

Best practices para GDPR, CCPA y privacy.

## GDPR

```javascript
// Verificar consentimiento
if (hasUserConsent()) {
  analytics.track('Page Viewed');
}

// Opt-out
function handleOptOut() {
  analytics.reset();
  localStorage.setItem('tracking_disabled', 'true');
}

// Data deletion
async function handleDataDeletion(userId) {
  await fetch(`/api/gdpr/delete-user-data/${userId}`, {
    method: 'DELETE'
  });
}
```

## PII Protection

```javascript
// ❌ No enviar sin procesar
analytics.identify(user.id, {
  credit_card: '4111111111111111',
  ssn: '123-45-6789'
});

// ✅ Hash o limitar
analytics.identify(user.id, {
  email: user.email, // OK con consentimiento
  credit_card_last4: user.card.slice(-4),
  has_ssn: !!user.ssn
});
```

## Próximos Pasos
- [Testing](testing.md)
- [Monitoring](monitoring.md)
