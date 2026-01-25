# Next.js

Implementación optimizada para Next.js con server-side tracking.

## Instalación

```bash
npm install @jitsu/nextjs
```

## App Router (_app.js)

```javascript
import { createClient, JitsuProvider, usePageView } from '@jitsu/nextjs';

const jitsuClient = createClient({
  tracking_host: "https://tracking.midas.com",
  key: "js.TU_KEY.AQUI"
});

function MyApp({ Component, pageProps }) {
  usePageView(jitsuClient); // Auto-track pageviews
  
  return (
    <JitsuProvider client={jitsuClient}>
      <Component {...pageProps} />
    </JitsuProvider>
  );
}
```

## Server-Side Tracking

```javascript
// pages/api/signup.js
import { createClient } from '@jitsu/nextjs';

const jitsu = createClient({
  key: "s2s.SERVER_SECRET.AQUI"
});

export default async function handler(req, res) {
  await jitsu.track('User Signup', {
    email: req.body.email
  });
  
  res.status(200).json({ success: true });
}
```

## Próximos Pasos
- [Configuración](configuracion.md)
- [Server-to-Server](../server-to-server.md)
