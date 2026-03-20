# React SDK

SDK optimizado para aplicaciones React.

## Instalación

```bash
npm install @jitsu/react
```

## Setup Básico

```javascript
// App.js
import { JitsuProvider, createClient } from '@jitsu/react';

const jitsuClient = createClient({
  writeKey: 'TU_WRITE_KEY',
  host: 'https://t.midas.media'
});

function App() {
  return (
    <JitsuProvider client={jitsuClient}>
      <YourApp />
    </JitsuProvider>
  );
}

export default App;
```

## Uso en Componentes

```javascript
import { useJitsu } from '@jitsu/react';

function ProductPage() {
  const { track, identify } = useJitsu();
  
  const handlePurchase = (product) => {
    track('product_purchased', {
      product_id: product.id,
      product_name: product.name,
      price: product.price
    });
  };
  
  return (
    <button onClick={() => handlePurchase(product)}>
      Comprar
    </button>
  );
}
```

## Track Automático de Pageviews

Con React Router:

```javascript
import { useJitsuPageView } from '@jitsu/react';
import { useLocation } from 'react-router-dom';

function App() {
  const location = useLocation();
  useJitsuPageView(location);
  
  return <YourRoutes />;
}
```

## Identificar Usuario

```javascript
import { useJitsu } from '@jitsu/react';
import { useEffect } from 'react';

function App() {
  const { identify } = useJitsu();
  const user = useAuth(); // Tu hook de autenticación
  
  useEffect(() => {
    if (user) {
      identify({
        id: user.id,
        email: user.email,
        name: user.name
      });
    }
  }, [user, identify]);
  
  return <YourApp />;
}
```

## Ejemplo Completo

```javascript
import { JitsuProvider, createClient, useJitsu } from '@jitsu/react';
import { useLocation } from 'react-router-dom';
import { useEffect } from 'react';

const jitsuClient = createClient({
  writeKey: 'TU_WRITE_KEY',
  host: 'https://t.midas.media'
});

function TrackingWrapper({ children }) {
  const location = useLocation();
  const { page } = useJitsu();
  
  // Track pageviews on route change
  useEffect(() => {
    page({
      path: location.pathname,
      search: location.search
    });
  }, [location, page]);
  
  return children;
}

function CheckoutButton({ product }) {
  const { track } = useJitsu();
  
  return (
    <button onClick={() => {
      track('checkout_started', {
        product_id: product.id,
        value: product.price
      });
    }}>
      Comprar Ahora
    </button>
  );
}

function App() {
  return (
    <JitsuProvider client={jitsuClient}>
      <TrackingWrapper>
        <YourRoutes />
      </TrackingWrapper>
    </JitsuProvider>
  );
}
```

## Próximos Pasos

- [Next.js](nextjs.md) - Para apps Next.js
- [JavaScript](javascript.md) - SDK vanilla
