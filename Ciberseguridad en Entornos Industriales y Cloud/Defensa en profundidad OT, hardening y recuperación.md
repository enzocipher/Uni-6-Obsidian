---
tags: [ciberseguridad, industrial, hardening, parches, recuperacion, iec62443]
materia: Ciberseguridad en Entornos Industriales y Cloud
unidad: 2
sesion: 7
ciclo: 6to
diapositivas: 51
actualizado: 2026-10-11
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546143_1/file/_76081592_1?courseId=_546143_1
---

# Defensa en profundidad OT, hardening y recuperación

## Objetivo y contexto

La sesión parte de un supuesto: **el atacante ya cruzó la frontera de red**. Se debe justificar qué otras capas protegen el proceso y cómo se recuperará la operación. Continúa las clases sobre zonas, conduits y acceso remoto, y cierra la Unidad 2 antes de la evaluación parcial.

Los productos de aprendizaje son un checklist de hardening y una tabla que vincule cada control con los requisitos de sistema (SR) o de componente (CR) de ISA/IEC 62443. Las 51 páginas incluyen separadores, láminas repetidas y ampliaciones; aquí se consolidan por concepto.

## 1. Capas con fallos diferentes

La profundidad depende de que varias barreras sigan funcionando cuando otra falle. Tres firewalls administrados con la misma consola y credencial pueden compartir el mismo punto de compromiso.

| Capa | Función | Relación docente con 62443 |
|---|---|---|
| Políticas y personas | Responsabilidades, formación y control de cambios | 2-1 |
| Seguridad física | Limitar quién llega al equipo y sus puertos | Programa 2-1 |
| Red y segmentación | Restringir comunicaciones entre zonas | FR5 y 3-2 |
| Host y componente | Reducir servicios y configurar el activo | 4-2 |
| Aplicación y lógica | Proteger software y programas de control | FR3, SR 3.4 |
| Monitoreo | Detectar cambios y comportamiento anómalo | FR6, SR 6.2 |
| Recuperación | Restaurar datos, configuraciones y operación | FR7 |

Pregunta de diseño: **si retiro esta capa, ¿qué sigue deteniendo al atacante?** La segmentación debe complementarse con identidad, autorización por tarea, monitoreo y recuperación.

### Del objetivo de zona al activo

La secuencia presentada es: zona → SL-T → SR del sistema → CR del componente → configuración de hardening → verificación del resultado.

- **SL-T:** nivel objetivo definido para la zona a partir del riesgo.
- **SL-C:** capacidad de seguridad declarada para un componente.
- **SL-A:** nivel alcanzado que debe evaluarse con evidencia.

Configurar un PLC ayuda a materializar sus capacidades; por sí solo no demuestra el SL-A de todo el sistema. Si la capacidad del equipo no alcanza el objetivo, se analizan controles compensatorios, aislamiento o reemplazo.

## 2. Dónde encaja cada parte de 62443

| Parte | Pregunta que organiza |
|---|---|
| 2-1 | ¿Cómo se gestiona el programa de seguridad? |
| 2-3 | ¿Cómo se coordina la gestión de parches? |
| 2-4 | ¿Qué se exige a proveedores de servicios? |
| 3-2 | ¿Cómo se evalúan riesgo, zonas y conduits? |
| 3-3 | ¿Qué requisitos cumple el sistema integrado? |
| 4-1 | ¿Cómo se desarrolla el producto de forma segura? |
| 4-2 | ¿Qué requisitos cumple cada componente? |

La presentación identifica 2-3 como informe técnico (TR): orienta la relación entre fabricante y propietario. Las tablas y numerales siguientes reproducen el material docente; para una cita formal se debe consultar la edición aplicable.

## 3. Hardening: reducir, configurar y verificar

1. **Reducir:** apagar servicios, puertos y cuentas innecesarios. Se relaciona con CR 7.7, funcionalidad mínima.
2. **Configurar:** sustituir valores de fábrica por una configuración aprobada. Se relaciona con CR 7.6.
3. **Verificar:** mantener inventario y línea base, comparar el estado real y corregir desviaciones. Se relaciona con CR 7.8 y el proceso de control de cambios.

En OT cada cambio requiere evaluar compatibilidad, probarlo, coordinarlo con el fabricante (OEM) y programarlo con Operaciones. Eliminar una función necesaria para controlar el proceso puede producir una indisponibilidad.

### Checklist por activo

| PLC | HMI | Estación de ingeniería (EWS) |
|---|---|---|
| Llave en RUN cuando corresponda | Modo quiosco | Equipo dedicado |
| Cambiar credenciales de fábrica | Cuentas por rol | Ubicación dentro de la zona autorizada |
| Desactivar Web, FTP o Telnet innecesarios | Controlar dispositivos USB | Credencial nominal |
| Proteger la lógica | Lista de aplicaciones permitidas | Proyectos versionados |
| Respaldo offline restaurable | Bloqueo por inactividad compatible con operación | Escaneo de medios extraíbles |

La EWS merece especial atención: **el PLC ejecuta la lógica y la estación de ingeniería la escribe**. Su compromiso puede permitir modificar varios controladores. La clase utiliza Stuxnet como ejemplo de esta relación.

### Requisitos destacados

| CR citado | Concepto de estudio |
|---|---|
| 7.7 | Funcionalidad mínima |
| 7.6 | Configuración de seguridad |
| 7.8 | Inventario de componentes |
| 1.7 y 1.11 | Contraseñas y gestión de intentos fallidos |
| 3.4 | Integridad del software y la información |
| 2.4 | Control del código móvil |
| 2.8 y 2.9 | Eventos auditables y capacidad de auditoría |

### Línea base y drift

La **línea base** es el estado aprobado y documentado de un activo. El **drift** es la desviación respecto de ese estado, especialmente cuando ocurre fuera del control de cambios.

Inventariar → definir → aplicar → comparar → corregir.

Indicador propuesto: porcentaje de activos que coinciden con su línea base. Debe acompañarse de evidencia, fecha y responsable; un porcentaje sin inventario fiable puede ocultar activos desconocidos.

### Casos citados en clase

- **TRITON, 2017:** se utiliza para discutir seguridad física del sistema instrumentado de seguridad y posición de la llave del controlador.
- **PIPEDREAM, 2022:** se relaciona con herramientas contra PLC y OPC UA y la necesidad de reducir funciones expuestas.

Son ejemplos docentes de capas de protección. Ningún control aislado garantiza evitar todos los pasos de esas campañas.

## 4. Parches en operación continua

La decisión combina el riesgo de explotación y el riesgo de detener el proceso. Las restricciones típicas son falta de ventana, dependencia del OEM, incompatibilidad, equipos sin soporte y costo de reinicio.

### Responsabilidades y ciclo

El fabricante informa compatibilidad de parches con el sistema; el propietario mantiene inventario, evalúa, prueba, despliega y verifica.

**Información → evaluación → prueba → despliegue → verificación.**

| Consecuencia | Explotación | Orientación del material |
|---|---|---|
| Alta | Fácil | Parche urgente o aislamiento, con decisión operativa controlada |
| Alta | Difícil | Próxima ventana y monitoreo reforzado |
| Baja | Fácil | Compensar y programar ventana |
| Baja | Difícil | Ventana normal documentada |

Es una matriz de discusión, no una autorización automática de cambio. La evaluación debe incluir exposición, compatibilidad y efecto sobre seguridad funcional.

### Si no se puede aplicar el parche

- Reducir quién puede alcanzar el servicio vulnerable.
- Apagar la función afectada si no es necesaria.
- Evaluar parcheo virtual mediante controles de red compatibles.
- Reforzar monitoreo y alertas.
- Aislar o reemplazar el activo cuando corresponda.

La vulnerabilidad permanece aunque disminuya su exposición. Cada compensación debe tener responsable, evidencia y fecha de revisión.

### Preparación de una ventana

| Antes | Durante | Después |
|---|---|---|
| Lista priorizada | Un cambio a la vez | Verificar versión |
| Prueba en entorno representativo | Criterio de aborto | Observar el proceso |
| Respaldo verificado | Operaciones presente | Actualizar línea base |
| Rollback escrito y probado | Respetar el tiempo disponible | Registrar lecciones |

La posibilidad de volver atrás se demuestra antes del cambio. El debate de clase pide completar: «Para consecuencia ___ y explotación ___, la decisión es ___; mientras tanto aplicamos ___; lo revisamos el ___».

WannaCry y NotPetya ilustran que un activo OT puede resultar afectado aunque la campaña no se dirija específicamente al control industrial. Los ejemplos de Rogers (2022) y Optus (2023) muestran también el impacto de cambios mal gestionados en disponibilidad; las fechas y descripciones proceden de la presentación.

## 5. Disponibilidad, redundancia y recuperación

La clase destaca cinco requisitos de FR7 en 3-3:

| SR | Propósito |
|---|---|
| 7.1 | Resistencia a denegación de servicio |
| 7.2 | Gestión de recursos |
| 7.3 | Respaldo |
| 7.4 | Recuperación y reconstitución |
| 7.5 | Energía de emergencia |

La redundancia mantiene servicio ante ciertos fallos. Si ambas réplicas comparten vulnerabilidad, credenciales o cambios defectuosos, un ataque puede afectar las dos. Se necesitan además respaldos protegidos, separación de dependencias y restauración probada.

### RPO y RTO

- **RPO (Recovery Point Objective):** pérdida máxima tolerable de información, expresada como tiempo hacia atrás desde el incidente. Ayuda a definir frecuencia y mecanismo de respaldo.
- **RTO (Recovery Time Objective):** tiempo objetivo para restablecer el servicio. Orienta preparación, recursos y procedimiento de recuperación.

Ejemplo de la clase:

| Hito | Hora |
|---|---|
| Último respaldo del SCADA | 02:00 |
| Ransomware cifra el SCADA | 05:30 |
| Planta vuelve a operar | 09:30 |

La pérdida real es de **3 h 30 min** y la recuperación real toma **4 h**. Cumplen los objetivos del ejercicio: RPO ≤ 4 h y RTO ≤ 6 h. Los objetivos se fijan antes; las duraciones observadas se comparan con ellos después.

La regla 3-2-1 se presenta como tres copias, dos medios y una copia fuera de sitio y desconectada. La restauración debe incluir programas de PLC, proyectos, configuraciones y dependencias necesarias, no solamente archivos de usuario.

## 6. Seguridad física

Controles propuestos: llave del controlador, gabinetes cerrados, puertos bloqueados, acceso a sala de control y protección de respaldos y repuestos. Añaden una barrera con un modo de fallo diferente al de una credencial o vulnerabilidad de red. Su funcionamiento depende también de custodia de llaves, autorizaciones y mantenimiento.

## 7. Aplicación a telecomunicaciones

| Planta industrial | Equivalente usado en telecom |
|---|---|
| PLC | Router, eNB/gNB u OLT |
| HMI | Consola NOC, NMS y gestor de alarmas |
| Estación de ingeniería | EMS/OSS que configura nodos |
| Zonas y conduits | Separación de planos de gestión, control y usuario |
| Acceso de proveedor | AAA con TACACS+ o RADIUS |
| SOC y estado del controlador | NOC, SOC y alarmas de red |
| Respaldo del programa | Respaldo de configuración y recuperación del core |

La analogía ayuda a identificar funciones; no declara equivalencia normativa entre una red telecom y un sistema industrial. El material menciona GSMA NESAS y 3GPP SCAS para equipos de red.

El dato nace en plataformas operativas: RAN, transporte, core y servicios como SMSC, DNS o AAA. Se expone de manera controlada mediante mediación, NEF o API Gateway hacia BSS, analítica, canales y socios. El EMS concentra riesgo porque administra numerosos nodos.

Para cambios se propone ventana de madrugada, MOP escrito, aprobación CAB, piloto y rollback probado. Para continuidad: core en varios sitios, N+1 o 1+1, rutas de fibra diversas, baterías y generadores. Kyivstar (2023) se usa como ejemplo de recuperación frente a un ataque destructivo.

## 8. Mapa de CR presentado

La ampliación docente organiza 58 CR de 4-2 en siete FR:

| FR | Tema | CR en la tabla |
|---|---|---:|
| 1, IAC | Identificación y autenticación | 14 |
| 2, UC | Control de uso | 13 |
| 3, SI | Integridad del sistema | 14 |
| 4, DC | Confidencialidad de datos | 3 |
| 5, RDF | Flujo de datos restringido | 4 |
| 6, TRE | Respuesta oportuna a eventos | 2 |
| 7, RA | Disponibilidad de recursos | 8 |

Incluye requisitos específicos según tipo: software (SAR), dispositivo embebido (EDR), host (HDR) y red (NDR), además de mejoras de requisitos (RE). Memorizar la cantidad no sustituye identificar aplicabilidad y evidencia para el componente concreto.

## Preguntas de repaso

1. ¿Por qué tres firewalls con la misma credencial pueden compartir un único punto de fallo?
2. ¿Qué diferencia hay entre SR, CR, SL-T, SL-C y SL-A?
3. ¿Por qué la EWS puede ser más crítica que una HMI?
4. ¿Cómo se detecta y corrige el drift?
5. ¿Qué evidencia permite posponer un parche con una compensación temporal?
6. ¿Qué debe contener un rollback antes de aprobar una ventana?
7. En el ejemplo del SCADA, ¿cuál es la pérdida real y cuál el tiempo real de recuperación?
8. ¿Qué amenazas afectan simultáneamente a dos equipos redundantes?
9. ¿Cómo se adapta la defensa en profundidad a un EMS y al core de una operadora?

## Referencias del material y conexiones

La bibliografía incluye IEC 62443-4-2, IEC TR 62443-2-3, 3-3 y 2-1; NIST SP 800-82 Rev. 3; CISA AA22-103A; Knapp y Langill (2014); GSMA NESAS, 3GPP SCAS y Open Gateway/CAMARA. Son referencias citadas por el docente, sin comprobación externa de ediciones en esta conversión.

- [[Segmentación industrial, zonas, conduits y seguridad funcional]]
- [[Convergencia IT y OT, IIoT y accesos remotos]]
- [[Defensa en Profundidad y Zero Trust]]
- [[Firewalls, IDS IPS, NAC e identidad y gestión de accesos]]
- [[Índice de Ciberseguridad en Entornos Industriales y Cloud]]

Las consignas de debate y evaluación se conservan como material académico para estudio.
