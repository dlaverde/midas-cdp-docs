# Google Tag Manager

Implementa el CDP de Midas sin modificar el código de tu sitio.

## Paso 1: Crear Tag HTML Personalizado

1. En GTM, ve a **Tags** → **New**
2. Selecciona **Custom HTML**
3. Pega el snippet del CDP de Midas

## Paso 2: Configurar Variable

1. **Variables** → **New** → **Constant**
2. Nombre: `Midas Write Key`
3. Valor: `js.TU_CLIENT_SECRET.AQUI`

## Paso 3: Configurar Trigger

- Trigger Type: **Page View**
- This trigger fires on: **All Pages**

## Tracking de Eventos

### Click en Botón

```html
<script>
  window.analytics.track('CTA Clicked', {
    button_text: '{{Click Text}}',
    button_url: '{{Click URL}}'
  });
</script>
```

Trigger: **Click - All Elements** con condiciones.

### Form Submit

```html
<script>
  window.analytics.track('Form Submitted', {
    form_id: '{{Form ID}}'
  });
</script>
```

## Próximos Pasos
- [Server-to-Server](server-to-server.md)
- [Casos de Uso](../casos-uso/ecommerce.md)
