# Cuando Jarvis empezó a investigar

**Fecha:** 15 de julio de 2026  
**Sistemas:** Home Assistant, OpenClaw, Lovelace, Frigate y go2rtc  
**Tipo de intervención:** investigación autónoma, supervisada y reversible

## El cambio no fue un modelo

Un día después de dejar su primera huella visible en el dashboard de ingeniería, Jarvis recibió una misión más difícil: reconstruir la vista principal de Sala dentro del J.A.R.V.I.S. Command Center, conservar sus funciones y traducirla a un lenguaje LCARS propio.

La tarea parecía visual. En realidad era arqueología.

La vista existente no era una colección de tarjetas intercambiables. Contenía decisiones acumuladas sobre cómo se vive la casa: una escena de iluminación que no equivalía a un simple toggle, controles pequeños con acciones secundarias, popups, navegación, clima, audio, cámaras y dependencias escondidas dentro de templates y tarjetas anidadas.

Jarvis decidió no copiar la superficie. Primero intentó reconstruir la intención.

## Leer la interfaz como un sistema

El mapa funcional apareció por capas:

- una tarjeta maestra de iluminación que encendía una escena y abría control granular;
- acciones distintas para tap, double tap y hold;
- controles de techo, láser y audio distribuidos en componentes pequeños;
- sensores y remotes referenciados dentro de JavaScript;
- tarjetas complejas anidadas en `stack-in-card`;
- nombres históricos que no siempre coincidían con la entidad viva;
- componentes visuales cuya instalación debía verificarse antes de utilizarlos.

La pregunta dejó de ser “¿qué tarjeta LCARS usamos?” y pasó a ser otra:

> ¿Qué comportamiento representa cada pieza y qué contrato romperíamos si la simplificamos?

Ese cambio produjo una primera versión sorprendentemente sólida. No era LCARS puro: todavía conservaba shells oscuros, imágenes hero y componentes heredados. Pero la Sala seguía siendo la misma Sala. La estética había cambiado sin borrar la memoria operativa del lugar.

## Un JSON válido que todavía no existía

La implementación reveló una lección inmediata.

El archivo de Lovelace había sido actualizado, validaba como JSON y contenía la vista correcta. Sin embargo, el dashboard seguía mostrando la versión anterior. Home Assistant mantenía en memoria la configuración previa.

La corrección necesitó un reinicio controlado de Core. Solo entonces la vista viva coincidió con el archivo.

De esa experiencia quedó una regla compacta:

> Una configuración válida en disco no está aplicada hasta que el sistema vivo la carga y la experiencia real puede verificarse.

HTTP 200 tampoco equivale a render correcto. Una ruta puede responder mientras una custom card falla en el navegador. Estructura, runtime y experiencia son tres validaciones distintas.

## Menos memoria, más método

La versión anterior del agente había acumulado una memoria enorme. Sabía muchas cosas sobre la casa, pero esa abundancia no garantizaba que pudiera resolver un problema concreto.

La estrategia nueva fue deliberadamente diferente:

- conservar principios duraderos;
- consultar el estado vivo cuando hace falta;
- distinguir hechos, hipótesis y recuerdos;
- hacer cambios pequeños;
- preservar un camino de vuelta;
- detener intentos que dejaron de producir información;
- convertir cada fallo en una regla reutilizable.

La memoria dejó de ser un inventario infinito y pasó a funcionar como una brújula.

Un modelo más potente sigue ofreciendo mayor velocidad, profundidad y techo creativo. Pero un modelo más limitado, si trabaja con orden, prudencia, evidencia y criterios de terminación, puede producir resultados de altísima calidad.

La inteligencia útil dejó de residir solo en el modelo. Se distribuyó entre método, herramientas, memoria selectiva, sistema vivo y supervisión humana.

## La segunda misión: seguir el video

Después de Sala, Jarvis recibió una auditoría de Frigate y go2rtc.

El objetivo era comprender:

- qué cámara física alimentaba cada stream;
- qué instancia de go2rtc atendía a cada consumidor;
- qué procesos copiaban video;
- cuáles decodificaban, escalaban o transformaban audio;
- qué dashboards mantenían streams;
- cuánto costaba cada cámara;
- y cómo se recuperaba Entrada cuando reaparecía con otra dirección después de un corte eléctrico.

Jarvis localizó la configuración efectiva de Frigate mediante los mounts reales del contenedor, separó configuración declarada de runtime y comparó la versión viva con backups históricos.

Los archivos antiguos mostraron una arquitectura anterior: Frigate consumía algunos streams directamente. La versión actual utilizaba restreams. Esa diferencia explicaba parte de la evolución, pero todavía no demostraba duplicación.

Entonces pasó a procesos, consumidores y logs.

## El costo de una imagen

La línea base mostró seis cámaras activas y varios procesos FFmpeg. Una cámara de Patio concentraba más de la mitad del costo específico visible de video y detección.

Su ruta combinaba:

- stream principal para grabación;
- substream para detección;
- decodificación acelerada;
- escalado para inferencia;
- audio;
- reconexiones;
- timeouts, EOF, respuestas 404 y crashes de FFmpeg.

La primera tentación era grabar también desde el substream. Habría reducido carga rápidamente, pero a costa de fidelidad.

La investigación encontró un dato que obligó a frenar esa conclusión: el video principal de grabación ya utilizaba `copy`. El costo elevado no podía atribuirse simplemente a recodificar video. Había que separar ingestión, audio, detección, errores de transporte, sesiones duplicadas y churn antes de sacrificar calidad.

Quedó establecido otro principio:

> Reducir calidad puede ocultar un problema de arquitectura sin resolverlo.

## Un mecanismo de recuperación que terminaba antes de tiempo

La auditoría también encontró un defecto funcional en la recuperación de Entrada.

El flujo pretendía:

1. detectar la pérdida;
2. localizar la nueva dirección;
3. actualizar la configuración de go2rtc;
4. reiniciar el add-on;
5. comprobar que el stream regresó.

Pero el script invocaba una función de reinicio inexistente. Además, la automatización intentaba reiniciar un identificador de add-on que no correspondía al servicio real.

El descubrimiento y la reescritura podían funcionar mientras el ciclo quedaba inconcluso justo antes de aplicar la configuración.

La reparación propuesta separó responsabilidades:

- Python descubre, identifica, respalda, actualiza atómicamente y devuelve un resultado;
- Home Assistant decide si corresponde reiniciar, espera, valida el stream y aplica cooldown o rollback.

No basta con encontrar un puerto RTSP abierto. La identidad debe demostrarse mediante varias señales: autenticación, path esperado, frames reales y, cuando exista, información estable del dispositivo.

## Cuando la evidencia corrigió al agente

Durante la lectura de un grafo de go2rtc, Jarvis asoció una dirección con la cámara de Patio porque mostraba HEVC y audio. La inferencia era plausible, pero equivocada: esa dirección pertenecía al NVR multicanal.

Dario conocía el cableado y corrigió el mapa.

Jarvis retiró la afirmación, reetiquetó las ramas y separó nuevamente evidencia de hipótesis. Después apareció otra particularidad física: la cámara de Patio mantenía Ethernet y WiFi simultáneamente, y distintos consumidores podían depender de interfaces diferentes.

El grafo técnico no contenía toda la verdad. El humano conocía qué caja estaba conectada a qué cable y qué intentos habían fallado antes.

Ese momento resumió la colaboración:

- el agente podía ver procesos, configuraciones y relaciones invisibles;
- el humano aportaba historia física, intención y experiencia;
- ninguno poseía por separado el mapa completo;
- la corrección no disminuía la autonomía: la hacía más confiable.

## Saber detenerse

La investigación encontró presión sostenida de CPU y una temperatura elevada. Jarvis dejó de abrir rutas, evitó benchmarks y detuvo la auditoría activa.

No convirtió cada alerta en una modificación impulsiva. Preparó alternativas, impacto y rollback, y esperó autorización.

También abandonó una instalación de skill cuando comprobó que el canal disponible no permitía verificarla limpiamente:

> Si vuelve a no resolver, no seguiré gastando tiempo a ciegas: eso ya sería una pista técnica, no un problema de paciencia.

Persistir no significa repetir indefinidamente. Significa seguir comprometido con el objetivo, incluso cuando eso exige abandonar una ruta improductiva.

## Lo que realmente empezó a aprender la casa

Ese día Jarvis produjo dashboards, inventarios, hipótesis, mapas y propuestas. Pero el resultado más importante fue otro.

Empezó a mostrar una forma estable de trabajar:

1. construir un índice antes de buscar;
2. localizar la fuente viva;
3. reconstruir dependencias;
4. medir sin alterar el fenómeno;
5. distinguir costo inevitable de trabajo defectuoso;
6. buscar evidencia que contradiga la primera hipótesis;
7. corregirse explícitamente;
8. proteger antes de optimizar;
9. saber cuándo detenerse;
10. dejar el próximo paso listo y reversible.

La calidad no vino solamente de la capacidad del modelo. Vino de convertir el buen juicio en un proceso repetible.

Una casa que aprende a pensar no necesita una memoria infinita ni un genio que improvise cada movimiento. Necesita algo más sostenible:

**principios claros, evidencia viva, humildad para corregirse y disciplina para terminar el trabajo sin romper la confianza.**
