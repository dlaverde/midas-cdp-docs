# Introducción a Funciones

Las funciones JavaScript permiten transformar, filtrar y enriquecer eventos antes de enviarlos a los destinos.

## Anatomía de una Función

```javascript
export default async function(event, { log, props, store }) {
  // Tu lógica aquí
  
  // Retornar evento modificado, null para filtrar, o array
  return event;
}
```

## Parámetros

- `event`: El evento entrante
- `log`: Función para logging
- `props`: Propiedades configurables
- `store`: Key-value store persistente

## Casos de Uso

- [Filtrado de Eventos](ejemplos/filtrado.md)
- [Enriquecimiento de Datos](ejemplos/enriquecimiento.md)
- [Normalización](ejemplos/normalizacion.md)
- [Deduplicación](ejemplos/deduplicacion.md)
- [Notificaciones](ejemplos/notificaciones.md)
- [PII Masking](ejemplos/pii-masking.md)

## Próximos Pasos
- [Ejemplos de Transformaciones](ejemplos.md)
- [NPM Packages](npm-packages.md)
