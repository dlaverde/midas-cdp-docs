# Performance y Optimización

Optimiza el rendimiento de tu tracking.

## Batch Events

```javascript
// ❌ Demasiados eventos
window.addEventListener('scroll', () => {
  analytics.track('Scrolled');
});

// ✅ Batching
const events = [];
window.addEventListener('scroll', () => {
  events.push({ depth: getScrollDepth() });
});

setInterval(() => {
  if (events.length > 0) {
    analytics.track('Scroll Interaction', { events });
    events = [];
  }
}, 5000);
```

## Debouncing

```javascript
import { debounce } from 'lodash';

const trackSearch = debounce((query) => {
  analytics.track('Search Performed', { query });
}, 500);

searchInput.addEventListener('input', (e) => {
  trackSearch(e.target.value);
});
```

## Próximos Pasos
- [Privacy y Compliance](privacy-compliance.md)
- [Testing](testing.md)
