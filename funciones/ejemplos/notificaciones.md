# Notificaciones

Envía notificaciones en tiempo real basadas en eventos.

## Notificación a Slack

```javascript
export default async function(event, { log, props, store }) {
  if (event.event !== 'user_signup') {
    return event;
  }
  
  const email = event.traits?.email || event.properties?.email;
  
  // Evitar duplicados
  const notified = await store.get(`notified:${email}`);
  if (notified) return event;
  
  try {
    await fetch(props.SLACK_WEBHOOK_URL, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        text: `🎉 New signup: ${email}`,
        blocks: [{
          type: 'section',
          text: {
            type: 'mrkdwn',
            text: `*New User*\n*Email:* ${email}\n*Plan:* ${event.properties?.plan || 'free'}`
          }
        }]
      })
    });
    
    await store.set(`notified:${email}`, true);
    log(`Slack notification sent for ${email}`);
  } catch (error) {
    log(`Error: ${error.message}`);
  }
  
  return event;
}
```

## Próximos Pasos
- [PII Masking](pii-masking.md)
- [NPM Packages](../../npm-packages.md)
