# The House That Learned to Think

> Una bitácora viva sobre una casa que dejó de limitarse a obedecer y empezó a observar, comprender y colaborar.

Este repositorio documenta la evolución de un hogar real construido sobre **Home Assistant**, automatización local, observabilidad, visión artificial y agentes de IA. No es un catálogo de dispositivos ni una colección de YAML aislado: es la historia técnica y humana de un sistema que fue adquiriendo contexto, memoria operativa y capacidad de actuar con criterio.

La casa comenzó resolviendo necesidades concretas: iluminación, presencia, cámaras, energía, clima, música y seguridad. Con el tiempo, la complejidad dejó de poder explicarse como una suma de automatizaciones. Hacía falta una nueva capa: un agente capaz de estudiar el sistema antes de intervenir, distinguir evidencia de ruido, proponer cambios reversibles y aprender del resultado.

Ese agente es **Jarvis**, operando mediante **OpenClaw** dentro de un entorno doméstico gobernado por Home Assistant.

## El momento que cambió el proyecto

El 14 de julio de 2026, Jarvis realizó su primera intervención autónoma visible sobre el dashboard **J.A.R.V.I.S. Engineering**.

Antes de modificarlo:

- inspeccionó las fuentes de observabilidad disponibles;
- verificó qué componentes visuales estaban realmente instalados;
- descartó entidades no confiables o no disponibles;
- seleccionó señales capaces de contar la salud real del host;
- creó un respaldo fechado;
- aplicó el cambio;
- validó la estructura local y remota;
- informó qué había comprobado y qué todavía requería validación humana.

El resultado no fue perfecto. Y precisamente por eso fue importante.

La primera captura reveló valores sin redondear, contraste insuficiente, etiquetas que no se aplicaron y componentes con más presencia visual que significado. La máquina había realizado una intervención técnicamente razonada; el humano aportó percepción, intención y criterio visual. La siguiente iteración nació de esa conversación.

**Ahí apareció la primera huella de verdad.**

→ [Leer: La primera huella de Jarvis](docs/02-la-primera-huella-de-jarvis.md)

## El día en que empezó a investigar

El 15 de julio, la prueba dejó de ser principalmente visual. Jarvis reconstruyó la semántica de la Sala antes de traducirla a LCARS y después siguió el recorrido de seis cámaras a través de Frigate, FFmpeg y dos capas de go2rtc.

Encontró configuración que validaba en disco pero todavía no vivía en Home Assistant, un mecanismo de recuperación que terminaba antes del reinicio, una cámara con carga desproporcionada y una hipótesis propia que tuvo que retirar cuando el conocimiento físico de la casa la contradijo.

Lo importante ya no fue una respuesta brillante. Fue la aparición de un método estable: observar, indexar, medir, corregirse, respaldar y saber detenerse.

→ [Leer: Cuando Jarvis empezó a investigar](docs/05-cuando-jarvis-empezo-a-investigar.md)

## Qué vive aquí

| Área | Propósito |
|---|---|
| [Origen](docs/00-origen.md) | Cómo Home Assistant dio lugar a OpenClaw y Jarvis |
| [Arquitectura](docs/01-arquitectura.md) | Capas, responsabilidades y flujo de decisión |
| [Primera huella](docs/02-la-primera-huella-de-jarvis.md) | La primera intervención autónoma documentada |
| [Principios](docs/03-principios.md) | Reglas para que la casa evolucione sin perder control |
| [Roadmap](docs/04-roadmap.md) | Próximos pasos técnicos y narrativos |
| [Método de investigación](docs/05-cuando-jarvis-empezo-a-investigar.md) | De la memoria extensa al criterio operativo |
| [Seguridad](SECURITY.md) | Qué nunca debe publicarse ni delegarse sin control |

## La idea central

Una casa inteligente no debería exigir que sus habitantes piensen como ingenieros para poder vivir en ella.

El objetivo no es automatizar cada gesto, sino reducir complejidad y construir un sistema que permita tomar mejores decisiones: cuándo intervenir, cuándo observar, cuándo preguntar y cuándo no hacer nada.

Este proyecto explora una forma de colaboración en la que:

- Home Assistant mantiene el estado y ejecuta;
- los sensores aportan evidencia;
- la observabilidad convierte señales dispersas en contexto;
- Jarvis investiga, propone e interviene dentro de límites;
- las personas conservan intención, validación y autoridad.

## Estado del proyecto

**Fase actual:** del hogar automatizado al hogar colaborativo.

La infraestructura está activa y en evolución. La documentación evita publicar secretos, credenciales, direcciones privadas o información que comprometa el entorno real.

---

Construido por **Dario “Daret” Gemi**, junto con Florencia, Jarvis y las inteligencias que ayudaron a convertir una colección de dispositivos en una casa que empezó a pensar.
