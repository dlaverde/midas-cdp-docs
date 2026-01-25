# Node.js Server-Side

Para aplicaciones Node.js, Express, Next.js API routes.

## Instalación

```bash
npm install @jitsu/sdk-js
```

## Express Integration

```javascript
const express = require('express');
const { jitsuClient, envs } = require('@jitsu/sdk-js');

const app = express();
const jitsu = jitsuClient({
  key: "s2s.TU_SERVER_SECRET.AQUI",
  tracking_host: "https://tracking.midas.com"
});

// Middleware de tracking
app.use(async (req, res, next) => {
  await jitsu.track('page_view', {
    env: envs.express(req, res)
  });
  next();
});

// Endpoint específico
app.post('/api/signup', async (req, res) => {
  await jitsu.track('user_signup', {
    env: envs.express(req, res),
    email: req.body.email
  });
  
  res.json({ success: true });
});
```

## Context Automático

El helper `envs.express()` extrae:
- URL, path, host
- User Agent, IP
- UTM parameters

## Próximos Pasos
- [Server-to-Server](server-to-server.md)
- [Next.js](javascript-sdk/nextjs.md)
