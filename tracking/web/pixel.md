# Pixel Tracking

Trackea eventos usando una imagen invisible 1x1, ideal para entornos donde JavaScript no está disponible.

## ¿Cuándo usar Pixel Tracking?

El pixel tracking es perfecto para:

- ✅ **Emails HTML** - Trackear aperturas de correos
- ✅ **Newsletters** - Medir engagement
- ✅ **Ambientes sin JavaScript** - Donde JS está bloqueado
- ✅ **Ads / Banners** - Trackear impresiones
- ✅ **Páginas de terceros** - Donde no puedes agregar código JS

⚠️ **Limitación**: Solo soporta HTTP GET, por lo que los datos deben ir en la URL.

## Cómo Funciona

1. Insertas una imagen invisible en tu HTML
2. La URL de la imagen contiene los datos del evento
3. Cuando se carga la imagen, el CDP registra el evento
4. El servidor devuelve un GIF transparente de 1x1 pixel

## Endpoint

```
https://t.midas.media/api/v1/p.gif
```

## Método 1: URL con Query Parameters

La forma más simple es pasar los datos como parámetros:

```html
<img 
  src="https://t.midas.media/api/v1/p.gif?token=TU_WRITE_KEY&event=email_opened&user_id=user_123&campaign=newsletter_enero"
  width="1" 
  height="1" 
  style="display:none;"
/>
```

**Parámetros:**
- `token` (requerido): Tu Write Key o Server Secret
- `event`: Nombre del evento
- Cualquier otro parámetro se convierte en propiedad del evento

## Método 2: Datos en Base64

Para eventos más complejos, codifica JSON en base64:

```html
<img 
  src="https://t.midas.media/api/v1/p.gif?data=eyJ0b2tlbiI6IlRVX1dSSVRFX0tFWSIsImV2ZW50IjoiZW1haWxfb3BlbmVkIiwidXNlcl9pZCI6InVzZXJfMTIzIiwicHJvcGVydGllcyI6eyJjYW1wYWlnbiI6Im5ld3NsZXR0ZXJfZW5lcm8ifX0="
  width="1" 
  height="1" 
  style="display:none;"
/>
```

**JSON original:**
```json
{
  "token": "TU_WRITE_KEY",
  "event": "email_opened",
  "user_id": "user_123",
  "properties": {
    "campaign": "newsletter_enero",
    "subject": "Ofertas de Enero"
  }
}
```

## Casos de Uso

### 1. Trackear Apertura de Email

```html
<!-- En tu email HTML -->
<html>
<body>
  <h1>Hola {{ user.name }}!</h1>
  <p>Contenido del email...</p>
  
  <!-- Pixel de tracking al final -->
  <img 
    src="https://t.midas.media/api/v1/p.gif?token=TU_KEY&event=email_opened&user_id={{ user.id }}&campaign=promo_verano"
    width="1" 
    height="1" 
    style="display:none;"
  />
</body>
</html>
```

### 2. Click en Email

```html
<a href="https://tutienda.com/promo?utm_source=email">
  <img src="https://t.midas.media/api/v1/p.gif?token=TU_KEY&event=email_clicked&user_id={{ user.id }}&link=promo" width="1" height="1" style="display:none;" />
  Ver Promoción
</a>
```

### 3. Impresión de Banner

```html
<!-- Banner publicitario -->
<div class="banner">
  <img src="banner.jpg" alt="Promo">
  <!-- Pixel de tracking de impresión -->
  <img 
    src="https://t.midas.media/api/v1/p.gif?token=TU_KEY&event=banner_viewed&campaign=display_q1&placement=homepage"
    width="1" 
    height="1" 
    style="display:none;"
  />
</div>
```

### 4. Newsletter con Múltiples Links

```html
<html>
<body>
  <!-- Pixel de apertura -->
  <img src="https://t.midas.media/api/v1/p.gif?token=KEY&event=newsletter_opened&user_id=123" width="1" height="1" style="display:none;" />
  
  <!-- Link 1 -->
  <a href="https://tienda.com/producto-a">
    <img src="https://t.midas.media/api/v1/p.gif?token=KEY&event=link_clicked&link_id=producto_a&user_id=123" width="1" height="1" style="display:none;" />
    Producto A
  </a>
  
  <!-- Link 2 -->
  <a href="https://tienda.com/producto-b">
    <img src="https://t.midas.media/api/v1/p.gif?token=KEY&event=link_clicked&link_id=producto_b&user_id=123" width="1" height="1" style="display:none;" />
    Producto B
  </a>
</body>
</html>
```

## Generación de Base64

### JavaScript

```javascript
const eventData = {
  token: 'TU_WRITE_KEY',
  event: 'email_opened',
  user_id: 'user_123',
  properties: {
    campaign: 'newsletter_enero'
  }
};

const base64Data = btoa(JSON.stringify(eventData));
const pixelUrl = `https://t.midas.media/api/v1/p.gif?data=${base64Data}`;

console.log(pixelUrl);
```

### Python

```python
import json
import base64

event_data = {
    'token': 'TU_WRITE_KEY',
    'event': 'email_opened',
    'user_id': 'user_123',
    'properties': {
        'campaign': 'newsletter_enero'
    }
}

json_str = json.dumps(event_data)
base64_data = base64.b64encode(json_str.encode()).decode()
pixel_url = f'https://t.midas.media/api/v1/p.gif?data={base64_data}'

print(pixel_url)
```

### PHP

```php
<?php
$eventData = [
    'token' => 'TU_WRITE_KEY',
    'event' => 'email_opened',
    'user_id' => 'user_123',
    'properties' => [
        'campaign' => 'newsletter_enero'
    ]
];

$jsonStr = json_encode($eventData);
$base64Data = base64_encode($jsonStr);
$pixelUrl = "https://t.midas.media/api/v1/p.gif?data={$base64Data}";

echo $pixelUrl;
?>
```

## Mejores Prácticas

### ✅ DO

```html
<!-- Pixel al final del body -->
<body>
  <h1>Contenido</h1>
  <p>Más contenido...</p>
  
  <!-- Pixel al final -->
  <img src="..." width="1" height="1" style="display:none;" />
</body>
```

```html
<!-- IDs únicos por usuario -->
<img src="https://t.midas.media/api/v1/p.gif?token=KEY&event=email_opened&user_id={{ unique_user_id }}" />
```

```html
<!-- Descriptivo en nombres de eventos -->
<img src="...?event=newsletter_january_2026_opened&campaign=promo" />
```

### ❌ DON'T

```html
<!-- ❌ No pongas el pixel al inicio -->
<body>
  <img src="..." />  <!-- Muy temprano -->
  <h1>Contenido</h1>
</body>
```

```html
<!-- ❌ No uses datos sensibles en la URL -->
<img src="...?email=user@example.com&password=123" />
```

```html
<!-- ❌ No hagas URLs muy largas (limite ~2000 caracteres) -->
<img src="...?property1=...&property2=...&property100=..." />
```

## Consideraciones de Privacidad

⚠️ **IMPORTANTE**: 

1. **Consentimiento**: Informa a usuarios que usas tracking pixels
2. **GDPR**: Respeta regulaciones de privacidad
3. **Datos Sensibles**: No envíes PII en URLs
4. **Opt-out**: Permite a usuarios desactivar tracking

## Limitaciones

| Aspecto | Limitación |
|---------|-----------|
| **Método HTTP** | Solo GET |
| **Tamaño URL** | ~2000 caracteres |
| **JavaScript** | No ejecuta código |
| **Context automático** | No captura user-agent, etc. |
| **Adblockers** | Pueden bloquear el pixel |

## Comparación: Pixel vs JavaScript SDK

| Feature | Pixel | JavaScript SDK |
|---------|-------|----------------|
| Ambientes sin JS | ✅ | ❌ |
| Emails HTML | ✅ | ❌ |
| Context automático | ❌ | ✅ |
| Datos complejos | ⚠️ Limitado | ✅ |
| User Agent | ❌ | ✅ |
| Cookies | ❌ | ✅ |
| Pageviews automáticos | ❌ | ✅ |

## Testing

### Verificar en Navegador

1. Abre tu HTML en el navegador
2. Abre DevTools → Network
3. Busca request a `p.gif`
4. Verifica status 200
5. Revisa query parameters

### Verificar en Email

1. Envía email de prueba a ti mismo
2. Abre el email
3. Verifica en tu warehouse que el evento llegó

### cURL Test

```bash
curl "https://t.midas.media/api/v1/p.gif?token=TU_KEY&event=test_pixel&test=true"
```

## Eventos Típicos para Email

```javascript
// Apertura
email_opened

// Click en link
email_link_clicked

// Desuscripción
email_unsubscribed

// Reenvío
email_forwarded

// Impresión de imagen
email_image_loaded
```

## Próximos Pasos

- [JavaScript SDK](javascript.md) - Para tracking más robusto
- [GTM](gtm.md) - Implementación sin código
- [API Reference](../../referencia/api.md) - Documentación completa

---

**Nota**: El pixel tracking es útil pero limitado. Para tracking completo, usa el [JavaScript SDK](javascript.md).
