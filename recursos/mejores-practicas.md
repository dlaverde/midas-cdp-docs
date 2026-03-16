# Mejores Prácticas

## Naming Conventions

### Eventos

✅ **Usa snake_case**
```javascript
product_viewed  // ✅
productViewed   // ❌
ProductViewed   // ❌
```

✅ **Formato: objeto_acción**
```javascript
button_clicked       // ✅
order_completed      // ✅
form_submitted       // ✅
```

### Propiedades

✅ **snake_case y descriptivo**
```javascript
{
  product_id: 'PROD-123',      // ✅
  product_name: 'Zapatos',     // ✅
  price: 99.99                 // ✅
}
```

## Identificación de Usuarios

✅ **Identifica lo antes posible**
```javascript
// Al login/signup
jitsu.identify({
  id: user.id,
  email: user.email
});
```

❌ **No uses email como ID**
```javascript
jitsu.identify({
  id: user.email  // ❌ Email puede cambiar
});
```

## Estructura de Eventos

✅ **Consistente**
```javascript
// Siempre mismas propiedades para mismo evento
jitsu.track('product_viewed', {
  product_id: 'PROD-123',
  product_name: 'Zapatos',
  price: 99.99,
  currency: 'USD'
});
```

❌ **Inconsistente**
```javascript
// A veces con category, a veces sin ella
jitsu.track('product_viewed', {
  product_id: 'PROD-123'
  // Faltan otras propiedades
});
```

## Performance

✅ **Carga async**
```html
<script src="..." defer></script>
```

✅ **Batch eventos en loops**
```javascript
// ❌ Mal
items.forEach(item => {
  jitsu.track('item_processed', item);
});

// ✅ Mejor
jitsu.track('items_processed', {
  items: items,
  count: items.length
});
```

## Privacy

✅ **No envíes PII sin consentimiento**
```javascript
if (userConsent.analytics) {
  jitsu.identify({
    email: user.email
  });
}
```

✅ **Hash datos sensibles**
```javascript
jitsu.track('payment_method_added', {
  card_last_4: '4242',  // ✅
  card_full: '...'      // ❌ Nunca
});
```

## Documentación

✅ **Mantén un Tracking Plan**

Documenta:
- Qué eventos trackeas
- Qué propiedades tiene cada uno
- Cuándo se disparan
- Quién los usa

Ejemplo:
```
Evento: product_viewed
Trigger: Cuando usuario ve producto
Properties:
  - product_id (string, required)
  - product_name (string, required)
  - price (number, required)
  - currency (string, required)
Usado por: Marketing, Product
```

## Testing

✅ **Test en staging primero**
```javascript
const jitsu = jitsuClient({
  writeKey: process.env.JITSU_KEY,
  // Usa diferente key para staging
});
```

✅ **Usa debug mode**
```javascript
jitsu.set('debug', true);
// Verás eventos en consola
```

## Monitoreo

✅ **Verifica que eventos llegan**
```sql
-- Query diario
SELECT 
  event,
  COUNT(*) as count
FROM events
WHERE DATE(timestamp) = CURRENT_DATE
GROUP BY event
ORDER BY count DESC;
```

✅ **Alerta en caídas**

Configura alertas si:
- Volumen de eventos cae >20%
- No llegan eventos en 1 hora
- Nuevos eventos no documentados
```
