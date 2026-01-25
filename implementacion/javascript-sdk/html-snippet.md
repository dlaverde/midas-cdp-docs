# HTML Snippet

Para sitios estáticos, WordPress, Webflow, etc.

## Instalación

Agrega antes del cierre de `</head>`:

```html
<script>
  !function(){
    var analytics=window.analytics=window.analytics||[];
    if(!analytics.initialize){
      if(analytics.invoked){
        window.console&&console.error&&console.error("Snippet included twice.");
      } else {
        analytics.invoked=!0;
        analytics.methods=["track","page","identify","reset"];
        analytics.factory=function(e){
          return function(){
            var t=Array.prototype.slice.call(arguments);
            t.unshift(e);
            analytics.push(t);
            return analytics;
          }
        };
        for(var e=0;e<analytics.methods.length;e++){
          var key=analytics.methods[e];
          analytics[key]=analytics.factory(key);
        }
        analytics.load=function(key){
          var t=document.createElement("script");
          t.type="text/javascript";
          t.async=!0;
          t.src="https://cdn.midas.com/analytics.min.js";
          var n=document.getElementsByTagName("script")[0];
          n.parentNode.insertBefore(t,n);
        };
        analytics._writeKey="TU_CLIENT_SECRET_AQUI";
        analytics.load("TU_CLIENT_SECRET_AQUI");
        analytics.page();
      }
    }
  }();
</script>
```

## Uso

```html
<script>
  // Track evento
  analytics.track('Product Purchased', {
    product_id: 'PROD-456',
    price: 99.99
  });
  
  // Identificar
  analytics.identify('user_123', {
    email: '[email protected]'
  });
</script>
```

## Próximos Pasos
- [React](react.md)
- [Configuración](configuracion.md)
