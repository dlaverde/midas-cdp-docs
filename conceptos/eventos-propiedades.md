# Eventos y Propiedades

Los eventos son el núcleo del CDP de Midas. Cada evento representa una acción que un usuario realiza.

## Anatomía de un Evento

```json
{
  "event": "Product Viewed",
  "userId": "user_123",
  "properties": {
    "product_id": "PROD-789",
    "price": 99.99
  }
}
```

## Tipos de Eventos

### Track
Rastrea cualquier acción:

```javascript
analytics.track('Button Clicked', {
  button_name: 'Sign Up'
});
```

### Page
Vista de página:

```javascript
analytics.page('Pricing');
```

### Identify
Identificación de usuario:

```javascript
analytics.identify('user_123', {
  email: '[email protected]',
  plan: 'premium'
});
```

## Properties vs Traits

- **Properties**: Atributos del evento (qué sucedió)
- **Traits**: Atributos del usuario (quién es)

## Próximos Pasos

- [Instalación](../comenzando/instalacion.md)
- [JavaScript SDK](../implementacion/javascript-sdk.md)
