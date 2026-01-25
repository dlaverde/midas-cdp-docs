# Content y Media

Tracking de engagement en sitios de contenido.

## Artículos

```javascript
// Artículo visto
analytics.track('Article Viewed', {
  article_id: 'art_123',
  title: 'Guía de Marketing Digital',
  category: 'Marketing',
  author: 'Juan Pérez',
  word_count: 2500
});

// Tiempo de lectura
analytics.track('Article Read', {
  article_id: 'art_123',
  read_percentage: 75,
  time_spent_seconds: 180
});

// Scroll depth
analytics.track('Scroll Depth', {
  page: '/blog/article-123',
  depth_percentage: 50
});
```

## Videos

```javascript
// Video started
analytics.track('Video Playback Started', {
  video_id: 'vid_456',
  video_title: 'Product Demo',
  duration_seconds: 300
});

// Video progress
analytics.track('Video Progress', {
  video_id: 'vid_456',
  progress_percentage: 25,
  current_time_seconds: 75
});

// Video completed
analytics.track('Video Playback Completed', {
  video_id: 'vid_456',
  completion_rate: 100
});
```

## Próximos Pasos
- [Mobile Apps](mobile-apps.md)
- [Marketing Attribution](marketing-attribution.md)
