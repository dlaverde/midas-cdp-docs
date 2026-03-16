# JavaScript SDK

SDK principal para sitios web y aplicaciones JavaScript.

## Instalación

### Via Script Tag

```html
<script 
  src="https://cdp.companydomain.m1das.app/p.js" 
  data-write-key="TU_WRITE_KEY"
  defer>
</script>
```

## API

### track()

Trackea un evento:

```javascript
// Event name only
jitsu.track("buttonClick");

// Event with properties
jitsu.track("itemPurchased", { price: 99 });
```

**Ejemplo real:**

```javascript
jitsu.track('product_purchased', {
  product_id: 'PROD-123',
  product_name: 'Zapatos Running',
  price: 89.99,
  currency: 'USD',
  quantity: 1
});
```

### identify()

Identifica al usuario:

```javascript
// Identify user: `xyz` as a userId, and additional properties (traits)
jitsu.identify('xyz', {
  name: 'Michael Scott',
  company: 'Dunder Mifflin',
})
//or just set a userId
jitsu.identify('xyz')
```

### page()

Trackea vista de página:

```javascript
//trigger page view with a custom name
jitsu.page("Page Name");

//trigger page view with a custom properties
jitsu.page({  propName: "propVal" });

//trigger page view with a name AND custom properties
jitsu.page("Page Name", {  propName: "propVal" });
```

## Eventos Automáticos

El SDK captura automáticamente:
- ✅ Pageviews
- ✅ User Agent
- ✅ IP
- ✅ UTM parameters
- ✅ Referrer

## Tracking en SPAs

Para Single Page Applications:

```javascript
// Detectar cambio de ruta
window.addEventListener('popstate', () => {
  jitsu.page({
    name: document.title,
    path: window.location.pathname
  });
});

// O con router
router.afterEach((to, from) => {
  jitsu.page({
    name: to.name,
    path: to.path
  });
});
```

## Próximos Pasos

- [API Reference](../../referencia/api.md) - Documentación completa
