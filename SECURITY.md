# Seguridad y publicación responsable

Este repositorio describe un sistema doméstico real. La documentación debe ser útil sin convertir la arquitectura en un mapa de acceso.

## Nunca publicar

- tokens de Home Assistant o servicios externos;
- claves API, contraseñas o secretos OAuth;
- claves SSH, certificados privados o archivos de credenciales;
- URLs privadas completas o endpoints autenticados;
- direcciones IP públicas, identificadores sensibles o datos personales innecesarios;
- streams, snapshots o imágenes que comprometan la privacidad de habitantes y visitantes;
- copias directas de archivos `.storage` que puedan contener datos internos.

## Antes de subir configuraciones

1. Sustituir secretos por referencias como `!secret`, variables de entorno o placeholders.
2. Revisar historial y metadatos, no solo el archivo visible.
3. Eliminar identificadores que no aporten al aprendizaje técnico.
4. Preferir ejemplos mínimos y sanitizados frente a volcados completos del sistema.
5. Confirmar que capturas no revelen URLs, nombres de usuarios, ubicaciones o cámaras privadas.

## Operación segura de agentes

Las intervenciones de Jarvis deben mantener:

- alcance explícito;
- mínimo privilegio;
- respaldo previo;
- cambios reversibles;
- validación antes de reiniciar servicios;
- reporte de acciones y limitaciones;
- confirmación humana para cambios destructivos, exposición externa o ampliaciones significativas de autoridad.

## Reporte responsable

Si detectás información sensible publicada por error, no la reproduzcas en un issue público. Contactá al propietario del repositorio por un canal privado y rotá inmediatamente cualquier secreto comprometido.
