# Enriquecimiento de Datos

Agrega información adicional a tus eventos.

## Enriquecer con Geo Data

```javascript
export default async function(event, { log, props }) {
  const ip = event.context?.ip;
  
  if (!ip) return event;
  
  try {
    const response = await fetch(
      `https://api.ipgeolocation.io/ipgeo?apiKey=${props.GEO_API_KEY}&ip=${ip}`
    );
    const geoData = await response.json();
    
    event.context.geo = {
      country: geoData.country_name,
      city: geoData.city,
      region: geoData.state_prov
    };
    
    log(`Enriched: ${geoData.city}, ${geoData.country_name}`);
  } catch (error) {
    log(`Error: ${error.message}`);
  }
  
  return event;
}
```

## Enriquecer con Datos de Usuario

```javascript
export default async function(event, { store, log }) {
  const userId = event.user_id;
  
  if (!userId) return event;
  
  // Obtener datos del store
  const userData = await store.get(`user:${userId}`);
  
  if (userData) {
    event.user_data = JSON.parse(userData);
    log(`Enriched with user data for ${userId}`);
  }
  
  return event;
}
```

## Próximos Pasos
- [Normalización](normalizacion.md)
- [Notificaciones](notificaciones.md)
