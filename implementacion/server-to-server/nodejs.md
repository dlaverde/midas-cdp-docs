# Node.js

Implementación server-to-server con Node.js.

## Código de Ejemplo

```javascript
const axios = require('axios');

async function trackEvent(eventName, userId, properties = {}) {
  try {
    const response = await axios.post(
      'https://tracking.midas.com/api/v1/s2s/event',
      {
        event_type: 'track',
        event: eventName,
        user_id: userId,
        timestamp: new Date().toISOString(),
        properties: properties
      },
      {
        headers: {
          'Content-Type': 'application/json',
          'X-Auth-Token': 's2s.TU_SERVER_SECRET.AQUI'
        }
      }
    );
    
    return response.data;
  } catch (error) {
    console.error('Error tracking event:', error);
    throw error;
  }
}

// Uso
trackEvent('user_upgraded', 'user_123', {
  from_plan: 'basic',
  to_plan: 'premium'
});
```

## Con Express

```javascript
app.post('/api/signup', async (req, res) => {
  await trackEvent('user_signup', req.user.id, {
    email: req.body.email
  });
  
  res.json({ success: true });
});
```

## Próximos Pasos
- [PHP](php.md)
- [Node.js Server-Side SDK](../nodejs-server-side.md)
