---
tags:
  - ciberseguridad
  - procesos
  - gobierno
  - nist_csf
materia: Procesos de Ciberseguridad
unidad: 1
sesion: 1
ciclo: 6to
diapositivas: 30
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546139_1/document/_75336016_1?view=content&state=view
---

# Sesión 1: Ciberseguridad como Proceso de Negocio y NIST CSF 2.0

La presentación reúne el bloque **1.0: Introducción al curso** y el bloque **1.1: Ciberseguridad como proceso de negocio y panorama del NIST CSF 2.0**.

## 1. Objetivo y Propósito

* Comprender la ciberseguridad como una función integrada al gobierno corporativo.
* Conocer los componentes del NIST CSF 2.0 y sus seis funciones.
* Relacionar gobierno, gestión de riesgos y controles operativos.
* Entender el proyecto integrador que se desarrolla durante el curso.

El propósito del curso es participar en la gestión de la ciberseguridad de una organización y comprender cómo se integra con las decisiones del negocio. La tecnología debe acompañarse de responsabilidades, procesos y supervisión.

---

## 2. Organización y Evaluación del Curso

| Unidad | Semanas | Contenido principal |
| :--- | :--- | :--- |
| 1 | 1 a 4 | Gobierno y gestión de riesgos: Govern e Identify |
| 2 | 5 a 8 | Zero Trust y procesos de Protect para identidades, endpoints, aplicaciones y datos; CIS Controls v8.1 |
| 3 | 9 a 12 | Detect y Respond; infraestructura y redes, SIEM/XDR, MITRE ATT&CK y NIST SP 800-61 |
| 4 | 13 a 16 | Recover, ISO 22301, regulación peruana e integración de NIST CSF con Zero Trust |

### Ponderaciones indicadas en la presentación

| Evaluación | Peso |
| :--- | ---: |
| Práctica Calificada 1 (PC1) | 10 % |
| Trabajo Parcial (TP) | 15 % |
| Evaluación Parcial (EA) | 15 % |
| Práctica Calificada 2 (PC2) | 10 % |
| Trabajo Final (TF) | 15 % |
| Evaluación de Desempeño (DD) | 15 % |
| Evaluación Final (EB) | 20 % |

---

## 3. Proyecto Integrador

Cada equipo asume el papel de una consultora de ciberseguridad contratada por una organización real con un incidente documentado entre **2019 y 2025**. El trabajo consiste en diseñar su modelo de gobierno y sus procesos de ciberseguridad a lo largo del curso.

El proyecto cubre las seis funciones del NIST CSF 2.0 sobre los dominios Zero Trust adoptados por el curso. Culmina con la defensa del diseño ante un comité ejecutivo simulado.

### Entregables y fechas dentro del curso

| Hito | Sesión o semana | Alcance |
| :--- | :--- | :--- |
| Formación de equipos | Sesión 1 | Organización del trabajo |
| Elección de organización | Sesión 4 | Presentar y justificar el caso |
| Entregable 1 | Semana 7 | Organización, gobierno, riesgos y dominios Identidad, Dispositivos, Aplicaciones y Datos |
| Entregable 2 y defensa | Semana 15 | Documento completo, dominios restantes, regulación, roadmap y defensa oral |

La presentación menciona la rúbrica **ABET Student Outcome 2**: diseño de la solución (10 puntos) y validación del impacto (10 puntos). También anuncia una estructura final de 12 secciones, pero no enumera esas secciones en estas diapositivas.

### Criterios para elegir la organización

1. Debe ser real, con un incidente de ciberseguridad documentado entre 2019 y 2025.
2. Debe existir suficiente información pública confiable: noticias serias o informes oficiales.
3. Su complejidad debe permitir abordar los seis dominios del proyecto.
4. El análisis debe contemplar al menos dos factores de impacto: salud, sociedad, economía, ambiente o cultura.
5. El caso no debe repetirse con otro equipo del curso.

---

## 4. Ciberseguridad como Proceso de Negocio

### Caso de clase: Target (2013)

Según el material, el atacante ingresó mediante un proveedor externo de aire acondicionado (HVAC) con acceso mal segmentado. El sistema de detección generó alertas, pero la organización no actuó a tiempo. La presentación señala **40 millones de tarjetas comprometidas** y consecuencias financieras y reputacionales.

El caso muestra que disponer de herramientas no garantiza una respuesta efectiva. La evaluación de terceros, la segmentación, la responsabilidad sobre las alertas y la toma de decisiones también forman parte de la seguridad.

### Discusión propuesta

La clase plantea debatir si ciberseguridad debe reportar solo a TI o también a Gerencia General. La pregunta busca conectar las decisiones técnicas con presupuesto, prioridades, riesgo y responsabilidad organizacional.

---

## 5. NIST Cybersecurity Framework 2.0

### 5.1 Concepto

El NIST CSF es un marco voluntario que ayuda a entender, gestionar y reducir el riesgo de ciberseguridad. Describe los resultados que un programa debe lograr y proporciona un lenguaje común entre especialistas y alta dirección. Puede aplicarse a organizaciones de distintos tamaños, sectores y niveles de madurez.

### 5.2 Evolución presentada

| Versión | Año | Énfasis |
| :--- | :--- | :--- |
| CSF 1.0 | 2014 | Infraestructura crítica, tras una orden ejecutiva de EE. UU. |
| CSF 1.1 | 2018 | Refuerzo del riesgo de cadena de suministro |
| CSF 2.0 | 2024 | Nueva función Govern y ampliación a organizaciones de cualquier tipo |

### 5.3 Tres componentes

| Componente | Qué representa | Uso |
| :--- | :--- | :--- |
| Core (núcleo) | Funciones, categorías y subcategorías de resultados | Define qué resultados se busca lograr |
| Profiles (perfiles) | Estado actual y estado objetivo | Identifica brechas y prioridades |
| Tiers (niveles) | Rigor y sistematicidad de la gestión del riesgo | Describe cómo se gestiona el riesgo |

La presentación indica **22 categorías y 106 subcategorías** dentro de las seis funciones. El curso trabaja principalmente con el Core y con los perfiles Current y Target.

### 5.4 Seis funciones del Core

| Función | Pregunta o propósito | Analogía del material |
| :--- | :--- | :--- |
| Govern | Estrategia, políticas, roles y supervisión | El cerebro |
| Identify | Qué activos, datos y riesgos existen | El mapa |
| Protect | Controles que previenen o limitan incidentes | El escudo |
| Detect | Cómo descubrir anomalías | Las alarmas |
| Respond | Qué hacer durante o después de un incidente | Los bomberos |
| Recover | Cómo restaurar la operación y aprender | La reconstrucción |

Govern e Identify acompañan transversalmente a las demás funciones. La clase profundiza luego en [[Govern y Gobierno de Ciberseguridad|Govern]] y [[Identify, Activos, Riesgos y Perfil de Madurez|Identify]].

### 5.5 Tiers

| Tier | Nombre | Características |
| :--- | :--- | :--- |
| 1 | Parcial | Prácticas informales e inconsistentes |
| 2 | Riesgo informado | Conciencia del riesgo, con aplicación poco consistente |
| 3 | Repetible | Prácticas formales, aprobadas y actualizadas periódicamente |
| 4 | Adaptativo | Mejora continua basada en aprendizaje y cambios del entorno |

El nivel adecuado depende del contexto y del riesgo. La presentación no exige que toda organización llegue automáticamente al Tier 4.

### 5.6 Current y Target Profile

* **Current Profile:** resultados y situación actual de ciberseguridad.
* **Target Profile:** resultados deseados según necesidades y apetito de riesgo.
* **Brecha entre perfiles:** base para construir el roadmap de mejora.

Un perfil describe resultados por función. Los Tiers describen las prácticas de gestión del riesgo que los acompañan.

---

## 6. Gobierno, Riesgo y Controles Operativos

| Elemento | Papel |
| :--- | :--- |
| Gobierno | Define estrategia, políticas y autoridad de decisión |
| Riesgo | Identifica qué se puede perder y cuán probable es |
| Controles operativos | Ejecutan la protección técnica y de proceso diariamente |

El gobierno orienta la estrategia de riesgo, el riesgo prioriza la protección y los controles ejecutan las decisiones. NIST CSF se relaciona con marcos como ISO 27001, COBIT, CIS Controls y MITRE ATT&CK.

## 7. Conclusiones Clave

1. La ciberseguridad requiere coordinación con el negocio, además de herramientas técnicas.
2. El Core organiza resultados en seis funciones complementarias.
3. Current y Target Profile permiten planificar mejoras justificadas.
4. El proyecto integrador conecta gobierno, riesgo y controles en un caso real.

## 8. Referencias del Material

* Pascoe, C., Quinn, S. y Scarfone, K. (2024). *The NIST Cybersecurity Framework (CSF) 2.0*, NIST CSWP 29.
* Kaplan, J. M., Bailey, T., O'Halloran, D., Marcus, A. y Rezek, C. (2015). *Beyond Cybersecurity: Protecting Your Digital Business*. Wiley.
* Video de clase: *Cyber Attack Explained: Target (2013)*.
