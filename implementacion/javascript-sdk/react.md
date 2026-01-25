# React

Implementación con React y hooks.

## Instalación

```bash
npm install @jitsu/react
```

## Configuración

```javascript
import { createClient, JitsuProvider, useJitsu } from '@jitsu/react';

const jitsuClient = createClient({
  tracking_host: "https://tracking.midas.com",
  key: "js.TU_KEY.AQUI"
});

function App() {
  return (
    <JitsuProvider client={jitsuClient}>
      <YourComponents />
    </JitsuProvider>
  );
}
```

## Uso en Componentes

```javascript
function ProductPage() {
  const { track } = useJitsu();
  
  const handlePurchase = (product) => {
    track('Product Purchased', {
      product_id: product.id,
      price: product.price
    });
  };
  
  return <button onClick={() => handlePurchase(product)}>Comprar</button>;
}
```

## Próximos Pasos
- [Next.js](nextjs.md)
- [Configuración Avanzada](configuracion.md)
