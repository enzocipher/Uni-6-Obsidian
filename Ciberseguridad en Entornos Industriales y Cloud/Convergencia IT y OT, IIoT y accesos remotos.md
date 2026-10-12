---
tags: [ciberseguridad, industrial, iiot, acceso-remoto]
materia: Ciberseguridad en Entornos Industriales y Cloud
unidad: 1
sesion: 6
ciclo: 6to
diapositivas: 53
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546143_1/file/_76024632_1?courseId=_546143_1
---

# Sesión 6: Convergencia IT y OT, IIoT y accesos remotos

## 1. Objetivo

Explicar motivadores y riesgos de convergencia, evaluar rutas IIoT y diseñar acceso remoto a HMI con controles trazables a IEC 62443.

## 2. Digitalización y transformación

Digitalizar cambia el soporte: papel → dato. Transformar modifica el proceso o la decisión usando ese dato. La cadena de frío integra IIoT que mide, IT que conserva, analítica que detecta, una persona que decide y un registro que comparte evidencia.

Los motivadores de convergencia son eficiencia/OEE, mantenimiento predictivo, trazabilidad/cumplimiento y soporte OEM. La arquitectura establece cómo obtener el beneficio manteniendo control sobre el riesgo.

| Supuesto anterior | Qué lo rompe | Respuesta |
|---|---|---|
| Aislamiento físico | Nube, VPN, USB y laptops | Conduits explícitos |
| Perímetro único | IIoT, proveedor, identidad y redes móviles | Inventario de rutas y zonas |
| Ciclo de vida estable | Equipos antiguos expuestos a amenazas actuales | Compensatorios y mantenimiento |
| Identidad local | Usuarios remotos, máquinas y servicios | Identidad nominal, alcance y revocación |

Cada ruta nueva se documenta con origen, destino, protocolo y propietario. Un firewall en un camino no controla una SIM o interfaz paralela.

## 3. Qué partes de IEC 62443 intervienen

| Parte | Aplicación |
|---|---|
| 2-4 | Requisitos del proveedor de servicios y acceso remoto |
| 3-2 | Evaluación de la nueva ruta como conduit |
| 3-3 | Autenticación, autorización, segmentación y monitoreo del sistema |
| 4-2 | Capacidad técnica del sensor/gateway |

## 4. IIoT y su superficie

IIoT mide variables de proceso y puede tener consecuencias OT aunque use tecnologías de consumo. Su vida útil, actualización y conectividad deben evaluarse junto con el proceso.

Un gateway con SIM propia puede pasar de nivel 0/1 directamente a Cloud: el firewall de planta no ve el tráfico, la IDMZ deja de mediar y aparece una ruta no evaluada.

| Superficie | Debilidad |
|---|---|
| Dispositivo | Credenciales por defecto y depuración abierta |
| Firmware | Actualización sin firma/verificación |
| Canal | MQTT/CoAP sin protección e identidad adecuadas |
| Gateway | Concentración de credenciales y doble salida |
| Nube/API | Tokens prolongados, permisos excesivos y aislamiento insuficiente |
| Suministro | Bibliotecas, integrador y claves reutilizadas |

Patrón del curso: **zona IIoT propia → camino único → broker/réplica en IDMZ → consumo Cloud**, con identidad individual y rotación. El flujo informa; si se requiere control de retorno, se analiza como otro conduit con su propio riesgo y autorización.

El material introduce NIST IR 8259/8259A como referencia para evaluar capacidades del dispositivo antes de comprar, junto con IEC 62443-4-2 y el soporte a largo plazo. Si el equipo no alcanza la capacidad requerida, evaluar compensatorios verificables en el conduit.

## 5. Tipos de acceso remoto

| Tipo | Riesgo | Control docente |
|---|---|---|
| Operación remota | Cambia proceso en vivo | Lectura por defecto; escritura aprobada |
| Ingeniería remota | Descarga lógica/configuración | Ventana y acompañamiento |
| Proveedor/OEM | Identidad y equipo externos | Bajo demanda, cuenta nominal y grabación |
| Monitoreo Cloud | Ruta permanente y posible retorno | Publicación controlada sin comandos de regreso |

Un permiso debe expresar tarea, activo y ventana: «lectura de diagnóstico del V-101, de 14:00 a 16:00, acompañado». El nombre de un proveedor no define alcance.

## 6. Arquitectura de referencia a HMI

1. Ticket con activo, tarea, ventana y aprobador.
2. VPN terminada fuera de OT con MFA.
3. Habilitación por un rol designado para la ventana.
4. Jump server en IDMZ, sesión registrada y escritorio controlado.
5. Conduit con un destino/protocolo y deny by default.
6. Sesión HMI de lectura salvo autorización de cambio, con operador acompañante.
7. Terminación, revocación temporal y archivo de evidencia.

| Control | Referencia presentada |
|---|---|
| Acceso desde red no confiable y aprobación | SR1.13 |
| Identidad de humanos/dispositivos | SR1.1/1.2 |
| Gestión de autenticadores | SR1.5/1.7 |
| Permisos por tarea | SR2.1 |
| Terminación de sesión | SR2.6 |
| Zonas y frontera | SR5.1/5.2 |
| Monitoreo y registro | SR6.2 |

Estos mapeos se conservan para estudio; la propia presentación pide verificar la edición al usar numerales formalmente.

### VPN

Protege transporte y puede autenticar el extremo, pero no sustituye límites de alcance, postura del equipo, grabación, autorización ni revocación. Si entrega acceso directo al segmento PLC, mantiene un riesgo de frontera aunque el túnel esté cifrado.

### Ocho controles del jump server

Ubicación IDMZ; origen único hacia planta; MFA y cuenta nominal; grabación y retención; restricciones de portapapeles/USB/unidades/navegación; herramientas aprobadas; cierre por inactividad o fin de ventana; hardening y parcheo propios.

## 7. Contrato y ciclo de vida del proveedor

Cláusulas docentes: identidad nominal; altas/bajas notificadas; ticket y ventana; MFA y no compartir credenciales; requisitos del equipo o escritorio provisto; registro y auditoría; notificación de incidentes; revocación al terminar contrato.

Ciclo: **alta → solicitud → aprobación → habilitación → acompañamiento → cierre → recertificación**. Revisar cuentas que ya no corresponden al contrato es parte del control continuo.

Antipatrones: escritorio remoto directo al HMI; usuario genérico OEM; acceso permanente; VPN que aterriza en control; laptop con interfaz OT y módem externo.

## 8. Casos y ejercicios

El material usa Ucrania 2015, Colonial Pipeline 2021, Oldsmar 2021 y Unitronics 2023 para relacionar acceso legítimo, cuentas heredadas, claves compartidas/default y exposición. Para Oldsmar conserva la incertidumbre posterior sobre si el evento fue intrusión o error humano. Son casos según la presentación, no hechos investigados de nuevo en esta conversión.

Respuesta de análisis: **causa raíz → control → requisito → evidencia**. Por ejemplo, acceso permanente → ticket/ventana/aprobación → SR1.13 → registros del permiso y cierre.

Ejercicio: OEM extranjero revisa una alarma de HMI en una embotelladora. Producir diagrama de todos los saltos, seis controles mínimos con FR/SR, reglas de conduit y condición de cierre. El material acepta lectura, dos horas, acompañamiento, MFA y grabación.

Trabajo grupal anunciado para el 6 de octubre: situación inicial con tres antipatrones; riesgo y SL-T; arquitectura; ocho controles y cláusulas; verificación; riesgo residual y costo. Rúbrica de veinte puntos: riesgo 5, diseño 5, trazabilidad 5, verificación/residual 3 y exposición 2. PDF, exposición de doce minutos y cinco de defensa según el documento.

## 9. Repaso y referencias

- Explicar qué protege una VPN y qué controles adicionales necesita.
- Identificar rutas IIoT que saltan el diseño.
- Distinguir acceso permanente de acceso bajo demanda.
- Diseñar y cerrar una delegación de acceso con alcance, plazo y evidencia.

Fuentes: CSA, *Future-proofing IoT Security*; NIST IR 8259 y 8259A; IEC 62443-2-4, 3-3 y 4-2; NIST SP 800-82 Rev. 3; CISA AA21-042A y alerta Unitronics; CSF 2.0.

Anterior: [[Segmentación industrial, zonas, conduits y seguridad funcional]]. Volver: [[Índice de Ciberseguridad en Entornos Industriales y Cloud]].
