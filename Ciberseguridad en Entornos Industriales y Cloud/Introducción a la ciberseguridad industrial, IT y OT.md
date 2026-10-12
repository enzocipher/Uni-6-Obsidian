---
tags: [ciberseguridad, industrial, ot, ics]
materia: Ciberseguridad en Entornos Industriales y Cloud
unidad: 1
sesion: 1
ciclo: 6to
diapositivas: 46
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546143_1/file/_75619554_1?courseId=_546143_1
---

# Sesión 1: Introducción a la ciberseguridad industrial, IT y OT

## 1. Objetivo

Diferenciar IT y OT por sus prioridades, consecuencias y ciclos de vida; reconocer los componentes de un sistema de control industrial y ordenar sus controles mediante NIST CSF 2.0.

## 2. El problema de la convergencia

El caso de apertura describe una embotelladora que conecta su historian a la nube, habilita acceso remoto al proveedor de PLC y publica una API hacia el ERP. Un ransomware entra por la red administrativa, alcanza la estación de ingeniería y detiene la línea durante 14 horas.

Los puntos a revisar son la ausencia de zona intermedia, la cuenta compartida del proveedor, los flujos de la API y la falta de trazabilidad. La solución requiere decisiones sobre segmentación, identidad, monitoreo y gestión de cambios.

| Entorno | Activos y finalidad | Consecuencia relevante |
|---|---|---|
| IT, tecnología de información | Datos, aplicaciones, usuarios y servicios digitales | Fuga o alteración de información, interrupción del negocio, incumplimiento |
| OT, tecnología operacional | PLC, HMI, SCADA y procesos físicos | Lesiones, daño de equipos, impacto ambiental, pérdida de producción |
| Cloud | Servicios, redes virtuales, identidades y APIs | Exposición de datos y servicios; acceso indebido por identidades |

El curso plantea una arquitectura conjunta IT/OT/Cloud. La salida de datos industriales hacia la nube debe diseñarse sin abrir un camino de comandos hacia la planta.

## 3. Prioridades y ciclo de vida

| Criterio | IT | OT |
|---|---|---|
| Prioridad típica | Confidencialidad, integridad, disponibilidad: CIA | Disponibilidad, integridad, confidencialidad: AIC |
| Vida de los activos | Renovación frecuente, versiones y parches regulares | Décadas de uso, obsolescencia y soporte limitado |
| Cambios | Compatibilidad relativamente amplia | Validación del fabricante y del proceso |
| Mantenimiento | Reinicios y ventanas más flexibles | Paradas escasas y operación continua |
| Seguridad | Protege información y servicios | Sostiene el proceso y la seguridad de las personas |

CIA y AIC son orientaciones para decidir; no sustituyen el análisis de riesgo. Un dato falso puede provocar una acción física peligrosa aunque el equipo siga disponible.

Un antivirus corporativo puede afectar una planta por latencia, incompatibilidad, reinicios o cuarentena de archivos. Un control debe evaluarse junto con operaciones, la criticidad del proceso y la certificación del fabricante.

### Ejercicio de decisión

Una vulnerabilidad crítica afecta servidores web IT y una HMI de una línea que opera 24/7:

1. Explicar qué riesgo introduce el parche inmediato.
2. Explicar qué riesgo introduce esperar la ventana de mantenimiento.
3. Proponer un control compensatorio.
4. Defender la decisión en términos de riesgo.

## 4. Qué es un ICS

Un **Industrial Control System** integra hardware, software, redes, sensores, actuadores y personas para controlar o supervisar un proceso físico.

| Concepto | Función |
|---|---|
| Sensor | Mide una variable física |
| Actuador | Ejecuta una acción: abrir una válvula, mover un motor |
| PLC | Lee entradas, ejecuta una lógica cíclica y escribe salidas |
| RTU | Adquiere datos y controla equipos remotos |
| HMI | Presenta el estado del proceso y permite operar |
| SCADA | Supervisa y adquiere datos de procesos geográficamente dispersos |
| DCS | Distribuye el control dentro de una planta de proceso continuo |
| Historian | Conserva series de tiempo, estados y eventos |

La vista funcional de una planta es: proceso físico → PLC/RTU → HMI/SCADA → historian/ingeniería → ERP, reportes y analítica.

### PLC y lenguaje Ladder

Un PLC es una computadora industrial preparada para condiciones difíciles, operación prolongada y respuesta determinista. Su scan lee sensores, ejecuta la lógica y acciona equipos.

El ejemplo visual conecta un sensor fotoeléctrico a la entrada **I1** y una lámpara a la salida **Q1**. En Ladder, un contacto normalmente abierto I1 gobierna la bobina Q1: con I1 = 0, Q1 = 0; al activarse la entrada, la lógica puede energizar la salida. Esto vincula una variable digital con una acción física.

## 5. Sectores, amenazas e impacto

Energía, manufactura, agua y minería incluyen subestaciones, generación, líneas de producción, robots, bombeo, tratamiento, molienda y transporte.

| Amenaza | Cómo afecta a OT |
|---|---|
| Ransomware | Puede alcanzar ingeniería o supervisión y detener producción |
| Acceso remoto débil | Proveedores o VPN sin control de acceso y trazabilidad |
| Credenciales compartidas | Impiden atribuir acciones en HMI o ingeniería |
| Malware y USB | Alcanzan equipos aislados durante mantenimiento |
| Cambios no autorizados | Alteran lógica, setpoints o recetas |
| Falta de visibilidad | Activos y tráfico sin inventario ni monitoreo |

La cadena de riesgo es: **entrada** por phishing, VPN, USB o proveedor → **movimiento** por credenciales y salto IT/OT → **manipulación** de HMI, PLC o lógica → **impacto** en producción, personas, equipos o ambiente.

El material introduce Stuxnet, Flame y Gauss como referencias históricas. Los casos industriales se desarrollan en [[Amenazas industriales, casos históricos y modelado de amenazas]].

## 6. NIST CSF 2.0 en IT, OT y Cloud

| Función | Ejemplos de la presentación |
|---|---|
| Govern, Gobernar | Política, responsabilidades y apetito de riesgo |
| Identify, Identificar | Inventario y criticidad de activos |
| Protect, Proteger | Firewall, MFA, hardening y backup |
| Detect, Detectar | SIEM, IDS y anomalías |
| Respond, Responder | Playbooks, comunicación y contención |
| Recover, Recuperar | Restauración, DRP y lecciones aprendidas |

En IT aparecen CMDB, EDR/SIEM, IAM y backup; en OT, inventario industrial, segmentación, acceso remoto y plan de parada; en Cloud, IAM, VPC/NSG, KMS y logging. Cambia la implementación de los controles según el entorno.

## 7. Errores que se deben reconocer

1. Parchar sin validar con operaciones o fabricante.
2. Escanear activamente sin conocer la sensibilidad OT.
3. Usar cuentas compartidas.
4. Conectar IT y OT sin segmentación ni DMZ.
5. No respaldar la configuración y lógica del PLC.

Seguridad OT combina riesgo cibernético, riesgo operacional y seguridad física. Apagar un equipo puede protegerlo y, al mismo tiempo, impedir que el negocio opere.

## 8. Organización del curso

La presentación asigna PC1 10%, TP 10%, EA 20%, PC2 10%, TF 15%, DD1 15% y EB 20%. El TF propone una arquitectura IT/OT/Cloud; DD1 se construye con participación, evidencias y avances. Las fechas son las anunciadas en la presentación, no un calendario actualizado.

## 9. Repaso y referencias

- Explicar por qué aplicar un control de IT directamente en OT puede aumentar el riesgo.
- Reconstruir la cadena desde un comando digital hasta el impacto físico.
- Diferenciar SCADA, DCS y PLC.
- Clasificar inventario, MFA, monitoreo y restauración en CSF 2.0.

Fuentes citadas: NIST CSF 2.0 (2024); NIST SP 800-82 Rev. 3 (2023) y Rev. 2 (2015); MITRE ATT&CK for ICS; prácticas de CISA; Knapp y Langill, *Industrial Network Security* (2014).

Video asignado: [Cybersecurity for Industrial Control Systems](https://www.youtube.com/watch?v=5Wpu6dsWEb8).

Siguiente: [[Arquitectura ICS y modelo de Purdue]]. Volver: [[Índice de Ciberseguridad en Entornos Industriales y Cloud]].
