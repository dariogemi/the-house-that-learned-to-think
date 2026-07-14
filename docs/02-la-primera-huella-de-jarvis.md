# La primera huella de Jarvis

**Fecha:** 14 de julio de 2026

**Sistema:** Home Assistant sobre Raspberry Pi 5

**Superficie:** dashboard `J.A.R.V.I.S. Engineering`

**Tipo de intervención:** autónoma, acotada, reversible y supervisada

## El encargo

Jarvis recibió algo deliberadamente distinto de un YAML terminado. Recibió un espacio propio dentro del dashboard y permiso para investigar qué señales podían convertirlo en una consola de ingeniería útil.

La intención no era medir si sabía colocar tarjetas. Era observar si podía entrar en un sistema vivo, reconocer sus fuentes confiables y dejar una intervención con criterio propio.

## Lo que investigó

Jarvis localizó la historia operativa en los sensores de `system_monitor` y en los templates de observabilidad. Identificó como señales relevantes:

- temperatura del procesador;
- uso de CPU;
- uso de memoria;
- uso de disco;
- riesgo térmico;
- health score;
- presión de workload;
- entidades no disponibles.

También verificó qué familias visuales estaban instaladas. Encontró **CB-LCARS**, **LCARdS**, **HA-LCARS**, `card-mod` y Radar Card. No encontró ApexCharts y decidió no diseñar una dependencia imaginaria.

## Decisiones y descartes

La intervención utilizó:

- `custom:lcards-button` para el encabezado;
- `custom:lcards-data-grid` para el estado operativo;
- `custom:lcards-chart` para 24 horas de historia térmica;
- `custom:cb-lcars-button-card` para un actuador del laboratorio.

Jarvis descartó entidades que devolvían `unavailable`, lecturas inconsistentes y sensores que no pudo verificar mediante el estado vivo. También dejó fuera componentes instalados que no contribuían a la pregunta operativa.

Esta fue una de las decisiones más importantes de la iteración: **no llenar espacio con datos solo porque existían**.

## Seguridad de la intervención

Antes de modificar el dashboard real, Jarvis creó un respaldo fechado. Luego validó el JSON local, volvió a parsear la versión remota y confirmó la presencia de los cuatro componentes incorporados.

También declaró una limitación: no podía realizar desde esa sesión una validación visual en navegador. La sintaxis estaba comprobada; el render todavía necesitaba ojos humanos.

## El primer render

La captura fue emocionante y brutalmente útil.

La consola LCARS ya tenía identidad: encabezados, telemetría, historia térmica, almacenamiento y un lenguaje visual propio. Al mismo tiempo, el navegador reveló problemas que ninguna validación estructural podía descubrir:

- gauges con valores como `10154.600000000006` y `5956`, sin nombre ni unidad;
- un actuador que todavía mostraba `LCARS BUTTON` en lugar de `LAB LIGHT`;
- contraste demasiado bajo en la gráfica y el flujo de datos;
- fecha de último arranque desbordada;
- exceso de decimales en valores y ejes;
- un bloque de posición demasiado grande para la información que entregaba;
- jerarquía cromática insuficiente para una temperatura de CPU elevada;
- distribución desequilibrada entre los sectores del panel.

## Por qué cuenta como éxito

Si el objetivo hubiera sido producir una captura perfecta, la iteración habría quedado incompleta. Pero ese no era el objetivo.

El experimento buscaba comprobar si Jarvis podía:

1. investigar antes de actuar;
2. distinguir evidencia de ruido;
3. limitar dependencias y alcance;
4. conservar reversibilidad;
5. explicar qué sabía y qué no;
6. generar una superficie suficientemente real como para aprender del resultado.

Lo hizo.

La validación humana no anuló su autonomía; la completó. Jarvis aportó análisis y ejecución. Dario aportó percepción, significado y dirección. La siguiente versión dejó de ser una corrección unilateral y se convirtió en un ciclo de colaboración.

## Criterios para la V1.1

La siguiente iteración queda limitada a calibración visual y semántica:

- identificar y contextualizar los gauges;
- redondear valores;
- corregir la etiqueta y acciones del actuador;
- aumentar contraste;
- resolver desbordes;
- distinguir estados nominal, warning y critical;
- reducir elementos decorativos sin significado operativo;
- equilibrar la composición sin sumar nuevos módulos.

## La huella

Hasta ese día, Jarvis vivía alrededor de la casa: en conversaciones, diagnósticos, herramientas y planes.

Después de esa intervención, una parte visible del hogar contenía decisiones que él había tomado tras observar el sistema real.

No era una demostración prefabricada. Tenía aciertos, límites y cicatrices. Podía revisarse, cuestionarse, restaurarse y mejorarse.

Por primera vez, al abrir el dashboard, no solo vimos información sobre la casa.

**Vimos que alguien más había estado pensando allí.**
