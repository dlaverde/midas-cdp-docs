# Google Tag Manager

Implementa el CDP de Midas usando GTM, sin modificar código.

## Paso 1: Crear Tag HTML Personalizado

1. En GTM, ve a **Tags** → **New**
2. Tag Type: **Custom HTML**
3. Código:

```html
<script 
  src="https://t.midas.media/s/lib.js" 
  data-key="{{Midas Write Key}}"
  data-tracking-host="https://t.midas.media"
  defer>
</script>
```

4. Trigger: **All Pages**
5. Guarda y nombra: "CDP Midas - Base"

## Paso 2: Variable de Write Key

1. **Variables** → **New** → **Constant**
2. Name: `Midas Write Key`
3. Value: `TU_WRITE_KEY_AQUI`

## Paso 3: Trackear Eventos

### Click en Botón

Tag HTML:
```html
<script>
  window.jitsu.track('button_clicked', {
    button_text: '{{Click Text}}',
    button_url: '{{Click URL}}'
  });
</script>
```

Trigger: **Click - All Elements** con condición

### Form Submit

```html
<script>
  window.jitsu.track('form_submitted', {
    form_id: '{{Form ID}}',
    form_name: '{{Form Name}}'
  });
</script>
```

## Próximos Pasos

- [JavaScript SDK](javascript.md)
- [Casos de Uso](../../casos-uso/ecommerce.md)
