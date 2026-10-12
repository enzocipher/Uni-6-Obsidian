---
tags: [ciberseguridad, industrial, purdue, arquitectura]
materia: Ciberseguridad en Entornos Industriales y Cloud
unidad: 1
sesion: 2
ciclo: 6to
diapositivas: 58
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546143_1/file/_75731489_1?courseId=_546143_1
---

# Sesión 2: Arquitectura ICS y modelo de Purdue

## 1. Objetivo

Ubicar componentes y flujos en una arquitectura industrial, distinguir niveles funcionales de zonas de seguridad y comparar una planta plana con una segmentada.

## 2. El lazo de control

**Sensor → controlador → actuador → proceso → realimentación al sensor.** El sensor mide; el controlador compara la medición con el setpoint y decide; el actuador ejecuta; el proceso cambia y se vuelve a medir.

- **Tiempo real:** los ciclos pueden repetirse en milisegundos.
- **Determinismo:** la respuesta debe ser predecible.
- **Consecuencia física:** una medición falsa produce una decisión sobre una realidad equivocada.

El PLC ejecuta un scan: leer entradas → ejecutar lógica → escribir salidas → diagnóstico → repetir. La lógica, los setpoints, el modo de operación y el firmware son elementos sensibles. El control básico que exige la sesión es una **golden config**, con lógica y configuración versionadas, restauración probada y gestión formal de cambios.

## 3. Componentes y consecuencias

| Componente | Función | Consecuencia de compromiso | Vector típico |
|---|---|---|---|
| Sensor | Medir variables | Decisiones con datos falsos | Manipulación de señal |
| Actuador | Ejecutar acciones | Movimiento no autorizado | Comando forzado |
| PLC/RTU | Ejecutar lógica | Cambio del comportamiento de la planta | Descarga de lógica o setpoint |
| HMI | Visibilidad y operación | Operación a ciegas | Credencial compartida |
| EWS | Programar controladores | Reescritura del proceso | Herramienta legítima infectada |
| Historian | Registrar y compartir datos | Puente IT/OT sin control | Conexión directa desde IT |
| SCADA/DCS | Supervisar y coordinar | Pérdida de control global | Movimiento lateral |

Los sensores pueden usar 4–20 mA, 0–10 V, HART, PROFIBUS PA o Foundation Fieldbus. Muchos instrumentos no admiten agentes, credenciales o parches convencionales; se protegen mediante acceso físico, redundancia, validación y controles alrededor de ellos.

### PLC frente a RTU

| Criterio | PLC | RTU |
|---|---|---|
| Ubicación | Planta, tablero o sala eléctrica | Pozo, subestación o bombeo remoto |
| Comunicación | Red industrial rápida y de baja latencia | Radio, celular o satélite de menor ancho de banda |
| Autonomía | Enlace permanente con supervisión | Puede operar y almacenar datos sin enlace |
| Lógica | Secuencias, enclavamientos y control rápido | Telemetría y control simple o por excepción |

### PLC frente a IIoT

El PLC cierra un lazo con latencia acotada; un nodo IIoT publica telemetría para consumo asíncrono. La presentación contrapone ciclos de vida de 15–25 años en PLC y 3–5 años en nodos IIoT. El PLC puede ocupar nivel 1 y un sensor IIoT estar físicamente en nivel 0/1 mientras publica hacia nivel 5.

El problema temporal central es el **jitter**, la variación del retardo. Un retardo predecible puede incorporarse al diseño; una antigüedad variable de las mediciones dificulta el control. La presentación explica TSN, DetNet y 5G privado URLLC como tecnologías que acercan la frontera, sin asumir que Internet proporciona un peor caso de tiempo real garantizado.

Ejemplos PLC: enclavamientos de prensa, dosificación, arranque de motores y parada coordinada. Ejemplos IIoT: vibración para mantenimiento, telemetría de tanques, energía y tableros OEE.

## 4. HMI, ingeniería e historian

- **HMI:** muestra el estado y permite acciones dentro de límites autorizados; requiere cuentas nominales, control de sesión y aplicaciones permitidas.
- **EWS:** contiene el software que programa y descarga lógica a PLC, DCS o SIS; concentra privilegios de ingeniería y acceso de proveedores.
- **Historian:** almacena valores, alarmas y eventos con marcas de tiempo; alimenta trazabilidad, OEE, regulación, mantenimiento y analítica.

Patrón del historian: **primario en nivel 3 → réplica de lectura en IDMZ 3.5 → consumidores IT/Cloud en 4–5**. El acceso de los consumidores se limita a la réplica. Deben definirse expresamente iniciador, dirección y permisos de cada flujo.

SCADA supervisa activos dispersos y depende de enlaces remotos; DCS distribuye el control dentro de una planta y abarca niveles 1, 2 y 3. Un DCS completo no se ubica en un único nivel.

## 5. Purdue, ISA-95 e IEC 62443

| Referencia | Aporte |
|---|---|
| Purdue Enterprise Reference Architecture | Jerarquía funcional entre empresa y manufactura |
| ISA-95 | Integración empresa/control, niveles 0–4 e intercambio de información |
| ISA-99 / IEC 62443 | Zonas, conduits y requisitos de seguridad |

La presentación utiliza la extensión de Purdue con niveles 0–5 y una IDMZ en 3.5. Nivel describe función; zona agrupa requisitos de seguridad; conduit controla comunicación entre zonas.

| Nivel | Función | Componentes |
|---|---|---|
| 0 | Proceso físico | Sensores, motores, válvulas y actuadores |
| 1 | Control básico | PLC, RTU, controladores DCS, SIS |
| 2 | Supervisión de área | HMI, SCADA, operador y alarmas |
| 3 | Operaciones de sitio | Historian, MES, dominio OT, ingeniería |
| 3.5 | IDMZ | Réplica, jump server, repositorio de parches y relay |
| 4 | Negocio de sitio | Planificación, logística, compras y administración |
| 5 | Empresa y servicios externos | ERP corporativo, cloud, proveedores e Internet |

Los niveles inferiores concentran exigencia temporal y consecuencia física. En 0–1 destacan protección física, validación, respaldo y control de quién programa. El SIS requiere separación del control básico. En 2–3 destacan identidades, inventario, aplicaciones permitidas, monitoreo y cambios. El MES coordina la ejecución de la producción y conecta la gestión con las operaciones.

## 6. IDMZ y flujos

La IDMZ funciona como punto de intercambio: las sesiones se terminan y se establecen conexiones separadas bajo control. Los protocolos de control no se publican hacia IT. El acceso remoto utiliza jump server, MFA, grabación, aprobación y una ventana definida.

La sesión formula dos patrones: réplica para consumo IT/Cloud y acceso administrativo intermediado. Sus frases sobre quién inicia conexiones deben interpretarse con el flujo concreto: documentar origen, destino, protocolo, iniciador y capacidad de lectura/escritura evita confundir publicación de datos con control remoto.

## 7. Cómo definir zonas

Cinco criterios:

1. Consecuencia compartida de un incidente.
2. Proceso o línea y sus dependencias.
3. Propietario, operador, horario y régimen de cambios.
4. Necesidad de comunicación en tiempo real.
5. Capacidad de los activos para soportar controles.

Dos PLC de nivel 1 pueden estar en zonas diferentes si uno controla envasado y otro refrigeración con amoníaco. Una ruta de red no equivale a confianza. Para cada conduit se define quién inicia, qué protocolo usa y qué acciones puede realizar.

## 8. Planta plana frente a segmentada

| Caso A: plana | Caso B: segmentada |
|---|---|
| PLC, HMI, historian, ERP y escritorios juntos | IT separado de niveles 0–3 por IDMZ |
| VPN del proveedor directa a planta | Jump server con MFA y grabación |
| ERP accede al historian primario | ERP consulta réplica |
| Sin inventario ni monitoreo | Inventario y monitoreo pasivo |
| Ransomware alcanza HMI/EWS y detiene la línea | El incidente se contiene en IT según el escenario |

IIoT, Cloud y 5G pueden saltar la jerarquía tradicional. Purdue sigue aportando una lectura de función y consecuencia; IEC 62443 define zonas y Zero Trust gobierna accesos.

## 9. Actividades y repaso

- Elaborar un mapa de planta con sus componentes y niveles.
- Comparar consecuencias en planta plana y segmentada.
- Explicar por qué un nivel puede contener varias zonas.
- Identificar al historian como puente y a la EWS como activo privilegiado.
- Preparar una exposición sobre 5G URLLC/IIoT o protocolos OT: conceptos, video menor de cinco minutos, ejemplo propio y conclusión defendible. El material presenta dos fechas distintas para esta actividad; consultar el anuncio docente para la fecha aplicable.

Referencias: ISA-95; Macaulay y Singer (2011); NIST SP 800-82 Rev. 3, secciones 2 y 5; IEC 62443-3-2; CISA Defense in Depth; Knapp y Langill (2014), capítulos 4 y 5; MITRE ATT&CK for ICS.

Anterior: [[Introducción a la ciberseguridad industrial, IT y OT]]. Siguiente: [[Protocolos industriales y requisitos de seguridad IEC 62443]]. Volver: [[Índice de Ciberseguridad en Entornos Industriales y Cloud]].
