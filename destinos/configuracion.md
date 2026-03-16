# Configuración de Destinos

Tu account manager configurará los destinos por ti.

## Proceso

1. **Proporciona credenciales** de tu warehouse
2. **Midas configura** la conexión
3. **Verifica** que los eventos llegan
4. **¡Listo!** Comienza a usar tus datos

## Verificar Configuración

Una vez configurado, verifica:

```sql
SELECT * FROM events 
ORDER BY timestamp DESC 
LIMIT 10;
```

Deberías ver tus eventos recientes.

## Soporte

¿Problemas con la configuración?
📧 [email protected]
