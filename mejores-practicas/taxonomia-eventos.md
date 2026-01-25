# Taxonomía de Eventos

Mantén un tracking plan documentado.

## Tracking Plan

Define cada evento con:

```yaml
event_name: Product Viewed
description: Cuando un usuario ve un producto
trigger: Page load de /products/:id
properties:
  product_id:
    type: string
    required: true
  product_name:
    type: string
    required: true
  price:
    type: number
    required: true
  currency:
    type: string
    required: true
    enum: [USD, EUR, COP]
```

## JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Product Purchased",
  "type": "object",
  "properties": {
    "product_id": {
      "type": "string",
      "description": "Unique product identifier"
    },
    "price": {
      "type": "number",
      "minimum": 0
    }
  },
  "required": ["product_id", "price"]
}
```

## Próximos Pasos
- [Identificación de Usuarios](identificacion-usuarios.md)
- [Performance](performance.md)
