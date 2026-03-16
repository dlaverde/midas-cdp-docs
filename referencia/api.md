# API Reference

Referencia completa de la API del CDP de Midas.

## jitsu.track()

Registra un evento.

**Sintaxis:**
```javascript
jitsu.track(eventName, properties)
```

**Parámetros:**
- `eventName` (string): Nombre del evento
- `properties` (object): Propiedades del evento

**Ejemplo:**
```javascript
jitsu.track('button_clicked', {
  button_name: 'Sign Up',
  page: '/landing'
});
```

## jitsu.identify()

Identifica al usuario.

**Sintaxis:**
```javascript
jitsu.identify(traits)
```

**Parámetros:**
- `traits` (object): Atributos del usuario
  - `id` (string, requerido): ID único del usuario
  - `email` (string): Email del usuario
  - Otros atributos personalizados

**Ejemplo:**
```javascript
jitsu.identify({
  id: 'user_123',
  email: '[email protected]',
  name: 'María García',
  plan: 'premium'
});
```

## jitsu.page()

Registra vista de página.

**Sintaxis:**
```javascript
jitsu.page(properties)
```

**Parámetros:**
- `properties` (object, opcional)
  - `name` (string): Nombre de la página
  - `category` (string): Categoría
  - Otros atributos

**Ejemplo:**
```javascript
jitsu.page({
  name: 'Product Detail',
  category: 'E-commerce'
});
```

## jitsu.setAnonymousId()

```javascript
//Set anonymous id of a user, such as ID of the visitor based on cookie
jitsu.setAnonymousId("xyz");
```

## Propiedades Reservadas

Estas propiedades tienen significado especial:

| Propiedad | Descripción |
|-----------|-------------|
| `userId` | ID del usuario |
| `anonymousId` | ID anónimo |
| `timestamp` | Timestamp del evento |
| `context` | Contexto automático |

## Context (Automático)

El SDK captura automáticamente:

```json
{
  "context": {
    "page": {
      "url": "https://ejemplo.com/pagina",
      "path": "/pagina",
      "title": "Título de la Página",
      "referrer": "https://google.com"
    },
    "userAgent": "Mozilla/5.0...",
    "ip": "192.168.1.1",
    "locale": "es-CO",
    "campaign": {
      "source": "google",
      "medium": "cpc",
      "name": "summer_sale"
    }
  }
}
```

No necesitas enviar esto manualmente.
