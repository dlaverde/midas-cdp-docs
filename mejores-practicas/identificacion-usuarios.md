# Identificación de Usuarios

Best practices para identificar usuarios.

## Anonymous ID

Se genera automáticamente y se mantiene en cookie.

## User ID

Solo cuando el usuario está identificado:

```javascript
// ❌ Incorrecto
analytics.identify('[email protected]'); // Email puede cambiar

// ✅ Correcto
analytics.identify('user_abc123', {
  email: '[email protected]'
});
```

## Momento del Identify

```javascript
// Al signup
function handleSignup(user) {
  analytics.identify(user.id, {
    email: user.email,
    name: user.name,
    created_at: user.createdAt
  });
  
  analytics.track('Account Created', {
    plan: user.plan
  });
}

// Al login
function handleLogin(user) {
  analytics.identify(user.id, {
    email: user.email,
    last_login: new Date().toISOString()
  });
}
```

## Próximos Pasos
- [Performance](performance.md)
- [Privacy y Compliance](privacy-compliance.md)
