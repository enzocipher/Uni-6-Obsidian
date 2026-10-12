---
tags: [ciberseguridad, industrial, amenazas, iec62443]
materia: Ciberseguridad en Entornos Industriales y Cloud
unidad: 1
sesion: 4
ciclo: 6to
diapositivas: 47
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546143_1/file/_75866536_1?courseId=_546143_1
---

# Sesión 4: Amenazas industriales, casos históricos y modelado de amenazas

## 1. Objetivo

Reconstruir incidentes OT, distinguir entrada de impacto físico, relacionar fallas con FR/SR y construir un modelo de amenazas con activos, actores, superficies y controles.

## 2. De FR a SR y RE

IEC 62443-3-3 organiza 51 requisitos del sistema en siete FR. La presentación distribuye 13 en FR1, 12 en FR2, 9 en FR3, 3 en FR4, 4 en FR5, 2 en FR6 y 8 en FR7.

| FR | Requisitos que desarrolla el material |
|---|---|
| FR1 | Usuarios/dispositivos, cuentas, identificadores, autenticadores, acceso inalámbrico, contraseñas, PKI, claves públicas, feedback, intentos fallidos, avisos, redes no confiables |
| FR2 | Autorización, inalámbrico, portátiles, código móvil, bloqueo y cierre de sesión, concurrencia, auditoría, almacenamiento, fallas de auditoría, tiempo y no repudio |
| FR3 | Comunicaciones, malware, verificación de funciones, software/datos, entradas, salida determinista, errores, sesión y auditoría |
| FR4 | Confidencialidad, persistencia y criptografía |
| FR5 | Segmentación, frontera de zona, P2P y particionamiento de aplicaciones |
| FR6 | Accesibilidad del log y monitoreo continuo |
| FR7 | DoS, recursos, backup, recuperación, energía, configuración, funciones mínimas e inventario |

Ejemplo docente: FR1 es la categoría; SR1.1 identifica/autentica a usuarios humanos; los RE refuerzan el requisito con identidad única o factores adicionales según el nivel aplicable. Para uso contractual, consultar la parte y edición del estándar, pues las tablas del curso simplifican obligaciones por SL.

El programa del propietario, 62443-2-1, incluye gobierno, activos, riesgos, accesos, proveedores, configuración, continuidad, monitoreo y mejora. La técnica requiere un proceso que la sostenga.

## 3. Casos históricos según la presentación

### Stuxnet, 2010

Objetivo: PLC Siemens de centrifugadoras en Natanz. El material describe entrada por USB a una red aislada, propagación mediante vulnerabilidades de Windows y certificados robados, alteración de frecuencias de variadores y ocultamiento mediante telemetría falsa. El impacto fue daño físico a centrifugadoras.

| Falla | FR | Control propuesto |
|---|---|---|
| Ejecución y medios sin control en EWS | FR1/FR2 | Control de USB y aplicaciones permitidas |
| Reprogramación sin detección | FR3 | Verificación de integridad de lógica y cambios |
| Telemetría falsa sin alerta | FR6 | Baseline y monitoreo pasivo |
| Movimiento hasta PLC sin barreras | FR5 | Zonas y conduits entre ingeniería y control |

Lección: el air gap no elimina medios extraíbles, mantenimiento ni ingeniería. El control de lógica y la visibilidad del proceso son esenciales.

### Industroyer / CrashOverride, 2016

El material describe acceso inicial y credenciales comprometidas, llegada a ICS y módulos que hablan IEC 101, IEC 104, IEC 61850 y OPC DA. La maniobra usa comandos de protocolo para operar interruptores. Incluye mecanismos de persistencia, destrucción y DoS; el impacto presentado es un corte en Kyiv.

| Falla | FR | Control propuesto |
|---|---|---|
| Emisor de comandos sin autenticación | FR1 | Protocolos seguros o validación de origen |
| Puente IT/OT con doble interfaz | FR5 | IDMZ y conduits explícitos |
| Barridos y comandos sin alerta | FR6 | Monitoreo industrial |
| Credenciales permiten acceso remoto | FR1/FR2 | MFA, bastión y grabación |

Lección: un atacante puede abusar de una función legítima del protocolo; no siempre necesita explotar un defecto de software para lograr el efecto físico.

### TRITON / TRISIS, 2017

Objetivo: controladores de seguridad Triconex. La sesión describe movimiento lateral a la red del SIS, compromiso de su estación de ingeniería, llave física en PROGRAM y protocolo TriStation sin autenticación. El propósito era manipular lógica de seguridad; un error del atacante provocó una parada segura y reveló el incidente.

| Falla | FR | Control propuesto |
|---|---|---|
| SIS alcanzable desde control | FR5 | Zona independiente y conduit muy restrictivo |
| Lógica de seguridad alterada | FR3 | Integridad y detección de descargas |
| Llave PROGRAM permanente | FR2 | RUN salvo mantenimiento y cambio autorizado |
| Reprogramación sin alerta | FR6 | Monitoreo del SIS y su EWS |

Lección: proteger el sistema que lleva el proceso a estado seguro exige una frontera independiente.

### Comparación

| Caso | Activo | Falla destacada | Consecuencia |
|---|---|---|---|
| Stuxnet | PLC de proceso | Integridad, FR3 | Daño de equipos |
| Industroyer | Equipos de subestación | Autenticación, FR1 | Corte eléctrico |
| TRITON | SIS | Segmentación, FR5 | Compromiso de la barrera de seguridad humana |

Los perfiles SL3–SL4 de la comparación son una lectura docente del adversario, no certificaciones de los incidentes. Los nombres e IDs ATT&CK del material deben contrastarse con el catálogo si se utilizan fuera del estudio.

## 4. Threat modeling OT

Cuatro preguntas:

1. **¿Qué construimos?** Diagramar activos, flujos, zonas, conduits y el sistema bajo consideración, SUC.
2. **¿Qué puede salir mal?** Enumerar amenazas y consecuencias físicas.
3. **¿Qué hacemos?** Seleccionar controles por riesgo; tratar, aceptar o transferir según decisión.
4. **¿Lo hicimos bien?** Validar y revisar ante cambios.

| Inventario | Contenido |
|---|---|
| Activos | PLC, RTU, IED, HMI, SCADA, historian, EWS, SIS, sensores y actuadores |
| Actores | Error humano, insider, atacante oportunista, crimen organizado, APT y proveedor comprometido |
| Superficies | Acceso remoto, USB, conduits, protocolos sin identidad y equipos dual-homed |

Árbol del ejemplo: **bomba arranca sin autorización** ← escribir coil FC05 ← alcanzar PLC TCP502 y descubrir registro. FR5 corta alcance; FR3 valida entradas; FR6 deja evidencia.

## 5. Marcos complementarios

CSF 2.0 organiza gobierno, identificación, protección, detección, respuesta y recuperación. SP 800-82 contextualiza la aplicación en OT. IEC 62443 aporta requisitos de programa, sistema y producto. El curso los combina en lugar de escoger uno como sustituto de los demás.

## 6. Laboratorio y evidencia

Se reutiliza OpenPLC .2, ScadaBR .3 y análisis .4 en 10.128.0.0/24. El objetivo adicional es modelar primero: dibujar SUC, identificar zonas y amenazas, proponer SL-T y verificar controles.

Fases: modelar → descubrir → capturar/mapear → demostrar escritura en la simulación → buscar el rastro → restringir origen, validar rango y mantener captura. Los comandos base están en [[Protocolos industriales y requisitos de seguridad IEC 62443]].

Entregable: **hallazgo | FR/SR | técnica ATT&CK | control | evidencia | estimación antes/después**. Las cifras SL del laboratorio sirven al razonamiento didáctico; aplicar una regla de red no acredita por sí solo un nivel completo.

Trabajo grupal: exponer segmentación, acceso remoto, hardening, monitoreo, USB/aplicaciones o recuperación, anclado a un incidente. Incluir amenaza, FR/SR, ubicación Purdue/zona, efecto operacional y SL-T justificado.

## 7. Repaso y referencias

- Diferenciar vector inicial, movimiento lateral e impacto físico en cada caso.
- Explicar por qué un SIS necesita zona propia.
- Pasar de una amenaza vaga a una cadena y controles verificables.
- Distinguir un FR, un SR y un RE.

Referencias de la sesión: Zetter, *Countdown to Zero Day* (2014); IEC 62443; MITRE ATT&CK for ICS; SP 800-82 Rev. 3; CSF 2.0; IEC 62443-3-2 y 3-3; análisis de Dragos, ESET y Mandiant/FireEye.

Anterior: [[Protocolos industriales y requisitos de seguridad IEC 62443]]. Siguiente: [[Segmentación industrial, zonas, conduits y seguridad funcional]]. Volver: [[Índice de Ciberseguridad en Entornos Industriales y Cloud]].
