# Pixel Tracking

Trackea eventos usando una imagen invisible 1x1, ideal para entornos donde JavaScript no está disponible.

> ℹ️ **Disponible desde**: Jitsu v2.8.2

## ¿Cuándo usar Pixel Tracking?

El pixel tracking es perfecto para:

- ✅ **Emails HTML** - Trackear aperturas de correos
- ✅ **Newsletters** - Medir engagement
- ✅ **Ambientes sin JavaScript** - Donde JS está bloqueado o restringido
- ✅ **Ads / Banners** - Trackear impresiones
- ✅ **Solo HTTP GET** - Cuando solo se permiten requests GET
- ✅ **Solo imágenes** - Cuando solo se permite embed de imágenes

⚠️ **Limitación**: Solo soporta HTTP GET, por lo que los datos deben ir en la URL.

## Cómo Funciona

1. Insertas una imagen invisible en tu HTML usando tag `<src>` o `<img>`
2. La URL de la imagen contiene los datos del evento
3. Cuando se carga la imagen, el CDP registra el evento
4. El servidor devuelve un GIF transparente de 1x1 pixel

## Pixel Endpoint

```
https://[your-jitsu-domain.com]/api/px/[event-type]
```

Para el CDP de Midas:
```
https://t.midas.media/api/px/[event-type]
```

**Ejemplo completo:**
```
https://t.midas.media/api/px/email_opened
```

## Query Parameters

Según la documentación oficial de Jitsu, estos son los parámetros disponibles:

| Parámetro | Descripción | Requerido |
|-----------|-------------|-----------|
| `writekey` | Write Key de tu Jitsu Stream configurado | ✅ Sí |
| `data` | JSON payload codificado en base64 | No |
| `path.to.node` | Path al nodo donde escribir el valor (formato JSON path) | No |
| `process_headers` | Boolean. Enriquece evento con datos de headers HTTP: Referrer y Cookies | No |
| `cookie_domain` | Cuando `process_headers=true`, configura Anonymous Id cookie (`__eventn_id`) para el dominio especificado | No |

## Método 1: Event Properties como Query Parameters

La forma más simple es pasar las propiedades del evento directamente como parámetros en la URL:

```html
<img 
  src="https://t.midas.media/api/px/email_opened?writekey=TU_WRITE_KEY&user_id=user_123&campaign=newsletter_enero"
  width="1" 
  height="1" 
  style="display:none;"
/>
```

**Ejemplo con más propiedades:**

```html
<img 
  src="https://t.midas.media/api/px/button_clicked?writekey=TU_WRITE_KEY&user_id=user_123&button_name=Get%20Started&page=/landing"
  width="1" 
  height="1" 
  style="display:none;"
/>
```

## Método 2: Datos en Base64

Para eventos más complejos, codifica el JSON payload en base64 usando el parámetro `data`:

```html
<img 
  src="https://t.midas.media/api/px/email_opened?writekey=TU_WRITE_KEY&data=eyJ1c2VyX2lkIjoidXNlcl8xMjMiLCJjYW1wYWlnbiI6Im5ld3NsZXR0ZXJfZW5lcm8iLCJzdWJqZWN0IjoiT2ZlcnRhcyBkZSBFbmVybyJ9"
  width="1" 
  height="1" 
  style="display:none;"
/>
```

**JSON original (antes de codificar):**
```json
{
  "user_id": "user_123",
  "campaign": "newsletter_enero",
  "subject": "Ofertas de Enero"
}
```

> **Nota**: El `writekey` va como query parameter, NO dentro del JSON payload codificado.

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
    src="https://t.midas.media/api/px/email_opened?writekey=TU_WRITE_KEY&user_id={{ user.id }}&campaign=promo_verano&email_id={{ email.id }}"
    width="1" 
    height="1" 
    style="display:none;"
  />
</body>
</html>
```

### 2. Click en Link de Email

```html
<a href="https://tutienda.com/promo?utm_source=email&utm_campaign=verano">
  <img 
    src="https://t.midas.media/api/px/email_link_clicked?writekey=TU_WRITE_KEY&user_id={{ user.id }}&link_name=promo_verano&destination=tienda" 
    width="1" 
    height="1" 
    style="display:none;"
  />
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
    src="https://t.midas.media/api/px/banner_viewed?writekey=TU_WRITE_KEY&campaign=display_q1&placement=homepage&banner_id=summer_sale"
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
  <img 
    src="https://t.midas.media/api/px/newsletter_opened?writekey=TU_KEY&user_id=123&newsletter_id=enero_2026" 
    width="1" 
    height="1" 
    style="display:none;"
  />
  
  <h1>Newsletter Enero 2026</h1>
  
  <!-- Link 1 con tracking -->
  <a href="https://tienda.com/producto-a">
    <img 
      src="https://t.midas.media/api/px/link_clicked?writekey=TU_KEY&user_id=123&link_id=producto_a&position=1" 
      width="1" 
      height="1" 
      style="display:none;"
    />
    Producto A
  </a>
  
  <!-- Link 2 con tracking -->
  <a href="https://tienda.com/producto-b">
    <img 
      src="https://t.midas.media/api/px/link_clicked?writekey=TU_KEY&user_id=123&link_id=producto_b&position=2" 
      width="1" 
      height="1" 
      style="display:none;"
    />
    Producto B
  </a>
</body>
</html>
```

### 5. Enriquecimiento con Headers HTTP

```html
<!-- Pixel con process_headers para capturar Referrer y Cookies -->
<img 
  src="https://t.midas.media/api/px/page_viewed?writekey=TU_KEY&process_headers=true&cookie_domain=.tudominio.com&page=/landing"
  width="1" 
  height="1" 
  style="display:none;"
/>
```

Esto capturará automáticamente:
- **Referrer** del header HTTP
- **Cookies** del navegador
- Creará/actualizará cookie `__eventn_id` para tracking anónimo

## Generación de Base64

### JavaScript

```javascript
const eventData = {
  user_id: 'user_123',
  campaign: 'newsletter_enero',
  subject: 'Ofertas Especiales'
};

const base64Data = btoa(JSON.stringify(eventData));
const writeKey = 'TU_WRITE_KEY';
const eventType = 'email_opened';

const pixelUrl = `https://t.midas.media/api/px/${eventType}?writekey=${writeKey}&data=${base64Data}`;

console.log(pixelUrl);
```

### Python

```python
import json
import base64
from urllib.parse import quote

event_data = {
    'user_id': 'user_123',
    'campaign': 'newsletter_enero',
    'subject': 'Ofertas Especiales'
}

json_str = json.dumps(event_data)
base64_data = base64.b64encode(json_str.encode()).decode()

write_key = 'TU_WRITE_KEY'
event_type = 'email_opened'

pixel_url = f'https://t.midas.media/api/px/{event_type}?writekey={write_key}&data={base64_data}'

print(pixel_url)
```

### PHP

```php
<?php
$eventData = [
    'user_id' => 'user_123',
    'campaign' => 'newsletter_enero',
    'subject' => 'Ofertas Especiales'
];

$jsonStr = json_encode($eventData);
$base64Data = base64_encode($jsonStr);

$writeKey = 'TU_WRITE_KEY';
$eventType = 'email_opened';

$pixelUrl = "https://t.midas.media/api/px/{$eventType}?writekey={$writeKey}&data={$base64Data}";

echo $pixelUrl;
?>
```

### Ruby

```ruby
require 'json'
require 'base64'

event_data = {
  user_id: 'user_123',
  campaign: 'newsletter_enero',
  subject: 'Ofertas Especiales'
}

json_str = event_data.to_json
base64_data = Base64.strict_encode64(json_str)

write_key = 'TU_WRITE_KEY'
event_type = 'email_opened'

pixel_url = "https://t.midas.media/api/px/#{event_type}?writekey=#{write_key}&data=#{base64_data}"

puts pixel_url
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
<img src="https://t.midas.media/api/s/s2s/pixel?token=KEY&event=email_opened&user_id={{ unique_user_id }}" />
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
3. Busca request a `/api/px/`
4. Verifica status 200
5. Revisa query parameters (`writekey`, propiedades del evento)

### Verificar en Email

1. Envía email de prueba a ti mismo
2. Abre el email
3. Verifica en DevTools → Network (si aplica)
4. Consulta tu warehouse para confirmar que el evento llegó

### cURL Test

```bash
# Test simple con query parameters
curl "https://t.midas.media/api/px/test_pixel?writekey=TU_WRITE_KEY&test=true&user_id=test_123"
```

```bash
# Test con data en base64
curl "https://t.midas.media/api/px/test_pixel?writekey=TU_WRITE_KEY&data=eyJ1c2VyX2lkIjoidGVzdF8xMjMiLCJ0ZXN0Ijp0cnVlfQ=="
```

```bash
# Test con process_headers
curl -H "Referer: https://google.com" \
     "https://t.midas.media/api/px/test_pixel?writekey=TU_WRITE_KEY&process_headers=true"
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

## Referencias

- [Documentación oficial de Jitsu Pixel API](https://docs.jitsu.com/sending-data/pixel) - Referencia completa y actualizada
- Disponible desde Jitsu v2.8.2

---

**Nota**: El pixel tracking es útil pero limitado. Para tracking completo con captura automática de contexto, usa el [JavaScript SDK](javascript.md).
