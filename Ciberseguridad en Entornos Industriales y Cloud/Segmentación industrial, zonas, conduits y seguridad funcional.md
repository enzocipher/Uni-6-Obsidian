---
tags: [ciberseguridad, industrial, segmentacion, sis]
materia: Ciberseguridad en Entornos Industriales y Cloud
unidad: 1
sesion: 5
ciclo: 6to
diapositivas: 57
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546143_1/file/_75965716_1?courseId=_546143_1
---

# Sesión 5: Segmentación industrial, zonas, conduits y seguridad funcional

## 1. Objetivo

Diseñar zonas, conduits e IDMZ, justificar SL-T mediante evaluación del riesgo, formular reglas de comunicación mínimas y distinguir la ciberseguridad de la seguridad funcional.

## 2. Del modelo de amenazas al diseño

El análisis comienza con SUC, activos, actores, superficies y consecuencias. ATT&CK for ICS aporta la vista del adversario y IEC 62443 la de los requisitos defensivos. Stuxnet se reconstruye desde USB y archivos Step7 hasta movimiento lateral, modificación de lógica y manipulación de la visión del operador.

En el árbol de la planta simulada, alcanzar TCP502 y enviar FC05 puede accionar la bomba: FR5 restringe el acceso; FR3 valida valores; FR6 conserva evidencia. Es necesario distinguir prevención, neutralización y detección.

## 3. SIS, SIF, SIL y SL

| Término | Significado |
|---|---|
| BPCS | Control básico que mantiene continuamente el proceso en su punto de operación |
| SIS | Sistema instrumentado que lleva el proceso a estado seguro ante una condición peligrosa |
| SIF | Función concreta de seguridad: detectar una condición y actuar dentro del tiempo requerido |
| SIL | Exigencia de integridad de una SIF frente a fallas peligrosas |
| SL | Nivel de requisitos de ciberseguridad frente al perfil de amenaza |

Un SIS puede ejecutar varias SIF, cada una con su propio SIL. Ejemplos: presión alta → cerrar entrada en menos de dos segundos; nivel bajo → detener bomba; temperatura alta → aislar y despresurizar.

Anatomía: sensores independientes → logic solver → elementos finales. Las fallas pueden ser medición congelada, lógica alterada o válvula trabada. TRITON atacó el logic solver.

El curso exige independencia del SIS frente al BPCS y zona separada. Compartir elementos sin analizar fallas comunes puede derribar ambas barreras.

### Métricas y tabla del material

- **PFDavg:** probabilidad media de falla peligrosa cuando se demanda una función de baja demanda.
- **PFH:** frecuencia de falla peligrosa por hora para funciones continuas o de alta demanda.
- **RRF:** factor de reducción del riesgo; en el ejemplo de baja demanda, RRF = 1/PFDavg.

| SIL | PFDavg, rango mostrado | RRF | PFH, por hora, rango mostrado |
|---|---|---|---|
| 1 | 10⁻² a 10⁻¹ | 10 a 100 | 10⁻⁶ a 10⁻⁵ |
| 2 | 10⁻³ a 10⁻² | 100 a 1 000 | 10⁻⁷ a 10⁻⁶ |
| 3 | 10⁻⁴ a 10⁻³ | 1 000 a 10 000 | 10⁻⁸ a 10⁻⁷ |
| 4 | 10⁻⁵ a 10⁻⁴ | 10 000 a 100 000 | 10⁻⁹ a 10⁻⁸ |

Ejercicio visual: si el tanque T-101 supera 10 bar, cerrar XV-101. Una reducción de 50 corresponde al rango SIL1; 500 a SIL2; 5 000 a SIL3; 50 000 a SIL4. Estas bandas son las de la presentación; los extremos y condiciones formales deben consultarse en la norma al especificar una SIF.

**SIL y SL no se intercambian:** uno expresa integridad funcional; el otro, requisitos de ciberseguridad. Un SIS requiere ambos análisis.

## 4. Nivel, zona y conduit

- **Nivel:** función del activo en Purdue/ISA-95.
- **Zona:** activos con requisitos comunes y frontera definida.
- **Conduit:** comunicación controlada entre zonas, con protocolo, dirección, acciones permitidas y SL-T.

La lista de zonas resulta del riesgo. Control básico y SIS pueden ocupar el mismo nivel funcional y requerir zonas diferentes.

FR5 se desarrolla en SR5.1 segmentación, SR5.2 frontera de zona, SR5.3 restricción P2P y SR5.4 particionamiento de aplicaciones. La separación limita que una falla local se vuelva global.

## 5. Proceso de evaluación y diseño

La presentación organiza los ZCR de la siguiente manera:

| Paso | Resultado esperado |
|---|---|
| ZCR1 | Definir SUC, activos, funciones y fronteras |
| ZCR2 | Evaluación inicial de alto nivel y peor consecuencia |
| ZCR3 | Particionar en zonas y conduits; separar SIS |
| ZCR4 | Evaluar amenazas, vulnerabilidades, consecuencia y probabilidad por zona/conduit |
| ZCR5 | Comparar con el riesgo tolerable |
| ZCR6 | Asignar SL-T según la evaluación |
| ZCR7 | Documentar requisitos y aprobación |

Esta es la secuencia didáctica del documento. Sus frases alternan entre «SL-T sale de ZCR4» y «se fija en ZCR6»: la evaluación alimenta la decisión, no basta con escoger un número. Para citar numerales formalmente, utilizar la edición correspondiente de IEC 62443-3-2.

La matriz docente 5×5 usa **consecuencia × probabilidad**. Colores: verde bajo, amarillo medio, naranja alto y rojo muy alto. El material asocia verde a SL-T1, amarillo a SL-T2, naranja a SL-T3 y rojo a SL-T3–4. Es una pauta del curso, no una conversión universal de cualquier matriz a SL.

SL-T es la meta; SL-C la capacidad; SL-A lo conseguido. Si falta capacidad, se evalúan compensatorios en el conduit y se comprueba el resultado con evidencia.

## 6. IDMZ y comunicaciones

| Componente IDMZ | Función |
|---|---|
| Historian espejo | Consultas IT/Cloud sobre réplica |
| Jump server | Acceso nominal, MFA, grabación y ventana |
| Repositorio de parches | Actualizaciones mediadas y controladas |
| Repositorio de firmas | Distribución sin salida individual a Internet |
| Relay/proxy | Terminar y reempaquetar el intercambio |
| Broker de aplicaciones | Publicar reportes sin exponer el servidor OT |

La regla central es **ninguna sesión IT→OT atraviesa la IDMZ de extremo a extremo**. El material también describe publicación desde OT hacia la réplica; por ello, su lema «OT nunca inicia hacia IT» se entiende como prohibición de rutas directas al exterior, no como sustituto de una matriz detallada de flujos.

| Conduit | Tráfico esperado |
|---|---|
| IT ↔ IDMZ | Consultas HTTPS a réplicas/tableros |
| IDMZ ↔ operaciones | Replicación y distribución controlada de parches |
| Operaciones ↔ supervisión | Lectura de datos SCADA/historian según servicio |
| Supervisión ↔ control | Comandos de HMI autorizada, dentro de límites |
| Control ↔ SIS | Intercambio mínimo de estado, según diseño independiente |

## 7. Firewall industrial y ACL

Un filtro industrial puede interpretar Modbus/DNP3 y distinguir function codes. Una regla de puerto no diferencia por sí sola lectura y escritura.

Principios: negar por defecto, abrir origen/destino/protocolo/dirección mínimos y registrar denegaciones. La disponibilidad del proceso debe evaluarse al diseñar el comportamiento ante falla del equipo de seguridad.

Ejemplo: permitir HMI→PLC TCP502 con acciones autorizadas; habilitar ingeniería solo en ventana; denegar otros orígenes y rutas PLC→IT. El registro alimenta FR6.

## 8. Laboratorio y evaluación

OpenPLC .2, ScadaBR .3 y análisis .4 en la VPC 10.128.0.0/24. Fases: comprobar red plana → demostrar escritura en la simulación → aplicar conduit → repetir y observar bloqueo.

```bash
# Reglas del ejemplo docente en el PLC simulado
iptables -A INPUT -p tcp --dport 502 -s 10.128.0.3 -j ACCEPT
iptables -A INPUT -p tcp --dport 502 -j DROP
```

La evidencia debe mostrar que el HMI sigue operando y que el origen no autorizado falla. Documentar zona, conduit, regla, FR/SR y resultado antes/después. Las cifras SL del ejercicio son estimaciones pedagógicas, no acreditación automática por instalar iptables.

Trabajo grupal: reconstruir Industroyer y TRITON con ATT&CK; identificar la técnica decisiva y el requisito que la mitiga; comparar causas y controles. Máximo diez diapositivas, quince minutos y dos fuentes APA según el material.

## 9. Repaso y referencias

Explicar nivel/zona/conduit; justificar SL-T; distinguir SIL de SL; describir sesión rota; explicar separación SIS/BPCS; escribir una ACL mínima y diferenciar DPI de filtrado por puerto.

Fuentes: IEC 62443-3-2 y 3-3; ISA GCA Zones and Conduits Guidance; NIST SP 800-82 Rev. 3; CISA Defense in Depth; Knapp y Langill, capítulos 5 y 9; CSF 2.0. El bloque funcional introduce IEC 61508/61511.

Anterior: [[Amenazas industriales, casos históricos y modelado de amenazas]]. Siguiente: [[Convergencia IT y OT, IIoT y accesos remotos]]. Volver: [[Índice de Ciberseguridad en Entornos Industriales y Cloud]].
