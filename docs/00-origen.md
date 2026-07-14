# El origen

## Antes de Jarvis, estaba la casa

El proyecto no comenzó con un agente de inteligencia artificial. Comenzó con una necesidad mucho más concreta: lograr que la tecnología doméstica dejara de sentirse como una colección de controles aislados.

Home Assistant se convirtió en el núcleo porque permitió reunir luces, sensores, cámaras, climatización, consumo energético, presencia, voz y entretenimiento bajo un mismo modelo de estado. Cada nueva integración resolvía algo, pero también ampliaba el sistema que había que comprender y cuidar.

La casa creció por capas:

1. **Control:** encender, apagar, regular y consultar.
2. **Automatización:** responder a eventos sin intervención manual.
3. **Contexto:** combinar presencia, hora, luz, consumo y estados humanos.
4. **Observabilidad:** entender salud, carga, errores y degradación.
5. **Inteligencia:** interpretar escenas, lenguaje y excepciones.
6. **Agencia:** investigar y proponer cambios dentro de límites explícitos.

## La complejidad como señal

El problema nunca fue que Home Assistant no pudiera hacer más. El problema fue que ya podía hacer tanto que comprender el conjunto exigía una nueva forma de trabajo.

Había automatizaciones que dependían de sensores, grupos de luces que representaban intenciones diferentes, cámaras con rutas de video distintas, servicios duplicados, entidades históricas y paquetes de observabilidad que contaban fragmentos de una misma historia.

La necesidad de OpenClaw y Jarvis nació ahí: no como reemplazo de Home Assistant, sino como una capa capaz de entrar al sistema, estudiarlo y razonar sobre él.

## De asistente a colaborador

Un asistente tradicional espera una orden precisa. Un colaborador puede recibir un objetivo, investigar las restricciones, elegir fuentes confiables, explicar sus decisiones y dejar el entorno en un estado verificable.

Eso es lo que se empezó a entrenar en Jarvis:

- observar antes de tocar;
- pedir permiso cuando la intención no esté clara;
- hacer cambios pequeños y reversibles;
- validar tanto la sintaxis como el comportamiento;
- reconocer lo que todavía no pudo comprobar;
- usar cada iteración para construir conocimiento operativo.

La pregunta dejó de ser “¿qué automatización podemos agregar?” y pasó a ser otra:

> ¿Cómo construimos una casa capaz de colaborar sin dejar de ser nuestra?

Este repositorio existe para documentar esa transición.
