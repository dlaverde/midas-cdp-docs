# Usando NPM Packages

Las funciones pueden usar cualquier paquete NPM.

## Ejemplo con Axios

```javascript
import axios from 'axios';

export default async function(event, { props }) {
  if (event.event === 'high_value_lead') {
    await axios.post(props.CRM_WEBHOOK, {
      email: event.traits.email,
      value: event.properties.estimated_value
    });
  }
  
  return event;
}
```

## Ejemplo con Lodash

```javascript
import _ from 'lodash';

export default async function(event) {
  // Limpiar properties nulos
  event.properties = _.omitBy(event.properties, _.isNil);
  
  return event;
}
```

## Ejemplo con Moment

```javascript
import moment from 'moment';

export default async function(event) {
  event.properties.formatted_date = moment(event.timestamp)
    .format('YYYY-MM-DD HH:mm:ss');
  
  return event;
}
```

## Próximos Pasos
- [Key-Value Store](key-value-store.md)
- [Ejemplos](ejemplos.md)
