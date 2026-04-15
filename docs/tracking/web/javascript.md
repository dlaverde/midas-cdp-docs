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
// Solo nombre del evento
jitsu.track("buttonClick");
// Evento con propiedades
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
// Identifica al usuario `xyz` con un userId y propiedades adicionales (traits)
jitsu.identify('xyz', {
  name: 'Michael Scott',
  company: 'Dunder Mifflin',
})
// O simplemente establece un userId
jitsu.identify('xyz')
```
### page()
Trackea vista de página:
```javascript
// Dispara una vista de página con un nombre personalizado
jitsu.page("Page Name");
// Dispara una vista de página con propiedades personalizadas
jitsu.page({  propName: "propVal" });
// Dispara una vista de página con nombre Y propiedades personalizadas
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
