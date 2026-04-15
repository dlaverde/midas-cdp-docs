# Estructura de Eventos

## Formato General

```json
{
  "event": "event_name",
  "userId": "user_123",
  "anonymousId": "anon_456",
  "timestamp": "2026-01-24T10:30:00.000Z",
  "properties": {
    "property1": "value1",
    "property2": "value2"
  },
  "context": {
    "page": {...},
    "userAgent": "...",
    "ip": "..."
  }
}
```

## Naming Conventions

### Eventos

Usa el formato: **objeto_acción**

✅ **Correcto:**
- `product_viewed`
- `button_clicked`
- `order_completed`
- `form_submitted`

❌ **Incorrecto:**
- `productView` (camelCase)
- `BUTTON_CLICK` (UPPER_CASE)
- `view product` (espacios)

### Propiedades

Usa `snake_case`:

✅ **Correcto:**
- `product_id`
- `product_name`
- `cart_total`

❌ **Incorrecto:**
- `productId` (camelCase)
- `product-name` (kebab-case)

## Tipos de Datos

| Tipo | Ejemplo | Uso |
|------|---------|-----|
| String | `"valor"` | Texto, IDs |
| Number | `99.99` | Precios, cantidades |
| Boolean | `true` | Flags |
| Array | `[1,2,3]` | Listas |
| Object | `{key: "val"}` | Objetos anidados |
| ISO 8601 | `"2026-01-24T10:30:00Z"` | Fechas |

## Eventos Estándar E-commerce

```javascript
// Producto visto
{
  "event": "product_viewed",
  "properties": {
    "product_id": "PROD-123",
    "product_name": "Producto",
    "price": 99.99,
    "currency": "USD",
    "category": "Categoría"
  }
}

// Producto agregado
{
  "event": "product_added",
  "properties": {
    "product_id": "PROD-123",
    "quantity": 1,
    "price": 99.99
  }
}

// Orden completada
{
  "event": "order_completed",
  "properties": {
    "order_id": "ORD-456",
    "revenue": 99.99,
    "tax": 8.00,
    "shipping": 5.00,
    "currency": "USD",
    "products": [...]
  }
}
```
