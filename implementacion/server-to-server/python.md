# Python

Implementación server-to-server con Python.

## Código de Ejemplo

```python
import requests
import json
from datetime import datetime

def track_event(event_name, user_id, properties=None):
    url = "https://tracking.midas.com/api/v1/s2s/event"
    headers = {
        "Content-Type": "application/json",
        "X-Auth-Token": "s2s.TU_SERVER_SECRET.AQUI"
    }
    
    payload = {
        "event_type": "track",
        "event": event_name,
        "user_id": user_id,
        "timestamp": datetime.utcnow().isoformat() + "Z",
        "properties": properties or {}
    }
    
    response = requests.post(url, headers=headers, json=payload)
    return response.json()

# Uso
track_event(
    event_name="subscription_created",
    user_id="user_123",
    properties={
        "plan": "premium",
        "amount": 999.99
    }
)
```

## Con Django

```python
from django.http import JsonResponse

def handle_signup(request):
    # ... tu lógica ...
    
    track_event("user_signup", user.id, {
        "email": user.email,
        "plan": user.plan
    })
    
    return JsonResponse({"success": True})
```

## Próximos Pasos
- [Node.js](nodejs.md)
- [Casos de Uso SaaS](../../casos-uso/saas-b2b.md)
