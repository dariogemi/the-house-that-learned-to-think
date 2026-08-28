# Arquitectura futura: AI Router, TTS/Briefings/Vision y fallback

**Estado:** Diseño / auditoría pendiente — NO IMPLEMENTADO
**Fecha:** 2026-08-27

## Objetivo

Diseñar una capa de abstracción para que Home Assistant no dependa de un único proveedor de IA. OpenAI no se elimina: actualmente no tiene saldo, pero se prevé recargarlo próximamente. La arquitectura debe permitir que vuelva a ser proveedor primario sin rehacer automatizaciones.

## Alcance

Auditar y posteriormente centralizar:

- LLM que generan texto.
- TTS y reproducción de audio.
- Briefings generados dinámicamente por IA.
- Análisis de imágenes/visión.
- Flujos LLM → TTS → media_player.
- Automatizaciones y scripts que implementan estos flujos. No se esperan blueprints relevantes.
- Node-RED, YAML, packages, config entries, REST commands y servicios indirectos.

## Proveedores a investigar

- OpenAI.
- Google.
- Nova Casa.
- BigPickle, especialmente sus modelos propios actualmente gratuitos.
- Otros proveedores ya instalados/funcionales y gratuitos, si aparecen durante la auditoría.

No asumir capacidades: cada modelo debe verificarse para LLM, visión/multimodal y/o TTS antes de asignarlo.

## Arquitectura conceptual

```text
AUTOMATIZACIÓN
      ↓
  AI ROUTER ─────────→ proveedor/modelo LLM
      ↓
 contenido
      ↓
  TTS ROUTER ────────→ proveedor TTS
      ↓
  media_player
```

Para visión:

```text
AUTOMATIZACIÓN → VISION ROUTER → modelo multimodal → análisis
```

Las automatizaciones no deberían conocer el proveedor concreto cuando sea posible.

## Fallback

El TTS debe contemplar una cadena configurable, inicialmente candidata a:

`OpenAI → Google → Nova Casa`

pero el orden final debe determinarse por capacidad, disponibilidad, coste, calidad y latencia reales.

También se quiere fallback para LLM/briefings y visión cuando técnicamente corresponda, con selección `AUTO` y posibilidad de seleccionar manualmente un proveedor/modelo para diagnóstico.

## Circuit breaker

No esperar un timeout de OpenAI en cada petición si se sabe que está caído o sin cuota.

- Detectar errores inmediatos de saldo/cuota, 429, 5xx, red y timeout.
- Marcar temporalmente proveedor como DOWN cuando corresponda.
- Enviar nuevas peticiones directamente al siguiente proveedor mientras esté DOWN.
- Tras un cooldown, hacer una prueba controlada (half-open).
- Si funciona, devolverlo automáticamente a PRIMARY/AUTO.
- El estado debe persistir razonablemente o reconstruirse de forma segura tras reinicio de Home Assistant.

## Latencia

La auditoría debe medir o estimar separadamente:

1. generación de texto;
2. generación de audio;
3. inicio de reproducción;
4. latencia añadida por fallback;
5. tiempo perdido por timeout.

Un error HTTP inmediato de saldo/cuota debería provocar un failover casi inmediato; un timeout debe evitarse mediante circuit breaker cuando sea posible.

## BigPickle

Investigar la configuración real y los modelos disponibles de BigPickle. Determinar cuáles son gratuitos y qué capacidades ofrecen. Aprovecharlos cuando sean adecuados, sin asumir que todos los modelos sirven para todas las tareas.

## Fase actual

Solo AUDITORÍA Y DISEÑO. No modificar producción, no eliminar integraciones y no reiniciar Home Assistant hasta disponer del inventario y arquitectura recomendada.

## Próximo paso

Ejecutar una auditoría completa de automatizaciones/scripts/configuración y producir un inventario de usos de LLM, TTS, briefings y visión, proveedores actuales, latencias, dependencias y propuesta de implementación incremental.
