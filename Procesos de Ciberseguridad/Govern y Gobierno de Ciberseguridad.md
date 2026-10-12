---
tags:
  - ciberseguridad
  - procesos
  - gobierno
  - raci
  - nist_csf
materia: Procesos de Ciberseguridad
unidad: 1
sesion: 2
ciclo: 6to
diapositivas: 24
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546139_1/file/_75653821_1?courseId=_546139_1
---

# Sesión 2: Govern y Gobierno de Ciberseguridad

## 1. Objetivo de la Sesión

* Entender la función Govern y sus seis categorías.
* Relacionar estrategia de riesgo, políticas y roles con decisiones organizacionales.
* Construir una matriz RACI y aplicar sus reglas de responsabilidad.
* Incorporar proveedores y terceros al gobierno del riesgo.

La [[Ciberseguridad como proceso de negocio y NIST CSF 2.0|Sesión 1]] explica las seis funciones del CSF. Govern establece la estrategia, las políticas, los roles y la supervisión que permiten operar el programa completo.

---

## 2. Caso de Clase: Uber (2016)

La presentación utiliza la cobertura de un hackeo que afectó a **57 millones de usuarios**, divulgado en 2017. El análisis se concentra en las decisiones de pagar y ocultar el incidente y en la ausencia de gobierno formal sobre decisiones de gran impacto.

Las preguntas del material son quién debía autorizar decisiones críticas, consultar a Legal, informar a los afectados y rendir cuentas a la Junta Directiva. El caso sirve para estudiar autoridad, responsabilidad, políticas y supervisión.

---

## 3. La Función Govern

Govern define:

* **Estrategia de riesgo:** postura conservadora o agresiva y criterios para aceptar riesgo.
* **Políticas:** reglas documentadas que orientan conductas, como acceso a datos o uso de dispositivos.
* **Roles y responsabilidades:** quién decide, ejecuta y supervisa.
* **Supervisión:** revisión del desempeño y ajuste de decisiones por la alta dirección.

### Seis categorías

| Código | Categoría | Contenido | Pregunta de estudio |
| :--- | :--- | :--- | :--- |
| GV.OC | Contexto organizacional | Misión, partes interesadas y obligaciones legales | ¿Qué hace la organización y qué la vuelve atractiva para un atacante? |
| GV.RM | Estrategia de gestión de riesgo | Apetito de riesgo y priorización de decisiones e inversiones | ¿Cuánto riesgo se acepta y quién lo decide? |
| GV.RR | Roles, responsabilidades y autoridad | Autoridad y rendición de cuentas desde la Junta hasta la operación | ¿Quién tiene autoridad final sobre decisiones críticas? |
| GV.PO | Política | Reglas formales, documentadas, aprobadas y comunicadas | ¿Existe una política para la situación o se improvisa? |
| GV.OV | Supervisión | Revisión periódica del programa y ajuste de estrategia | ¿La Junta recibe reportes regulares del riesgo? |
| GV.SC | Riesgo de cadena de suministro | Riesgo de proveedores y terceros con acceso a sistemas o datos | ¿Qué acceso tienen y quién los supervisa? |

### 3.1 Contexto organizacional (GV.OC)

El diseño del programa parte de la misión, clientes, reguladores, socios y obligaciones de la organización. Un banco y una biblioteca tienen distintos activos, consecuencias y necesidades de seguridad.

### 3.2 Estrategia de gestión de riesgo (GV.RM)

El apetito de riesgo orienta cuánto riesgo se acepta y cómo se equilibran inversiones en seguridad con otros objetivos. El material conecta el acceso amplio del proveedor de HVAC de Target con una decisión de riesgo que existía aunque no se hubiera explicitado.

### 3.3 Responsabilidades y autoridad (GV.RR)

La autoridad debe quedar definida antes de una crisis. La matriz RACI traduce esta categoría en responsables, aprobadores, consultados e informados para cada actividad.

### 3.4 Política (GV.PO)

Las políticas deben estar escritas, aprobadas y comunicadas. La clase usa la divulgación de incidentes de Uber para mostrar el riesgo de dejar una decisión crítica a una sola persona.

### 3.5 Supervisión (GV.OV)

Alta dirección y Junta revisan periódicamente el programa y modifican la estrategia con base en resultados. El material relaciona esta categoría con la supervisión insuficiente en Target y Uber.

### 3.6 Cadena de suministro (GV.SC)

La gestión de terceros abarca evaluación previa a la contratación, definición del acceso permitido y supervisión posterior. El riesgo continúa después de firmar un contrato, especialmente si el proveedor mantiene acceso a datos o sistemas.

---

## 4. Matriz RACI

| Letra | Rol | Significado |
| :--- | :--- | :--- |
| R | Responsable | Ejecuta el trabajo |
| A | Aprobador / responsable final | Tiene la rendición de cuentas final |
| C | Consultado | Aporta opinión antes de tomar decisiones |
| I | Informado | Recibe información sobre avances o decisiones |

La distinción central es que ejecutar una actividad (R) y responder por su resultado (A) son responsabilidades diferentes.

### Construcción paso a paso

1. Enumerar actividades o decisiones como filas.
2. Identificar personas, áreas o roles como columnas.
3. Asignar R, A, C o I a cada relación actividad-rol que corresponda.
4. Verificar que cada actividad tenga **exactamente un A y al menos un R**.
5. Validar la matriz con los involucrados antes de darla por definitiva.

### Ejemplo del docente: actualizar la política de contraseñas

| Rol | Asignación |
| :--- | :--- |
| CISO | A |
| Gerente de TI | R |
| Legal | C |
| Empleados | I |

Este ejemplo muestra un esquema para una actividad concreta. La asignación debe ajustarse a la autoridad real de la organización.

---

## 5. Actividades Propuestas en Clase

### Organigrama de seguridad

En una empresa ficticia, el equipo debe definir quién autoriza un pago de rescate, quién decide informar a usuarios afectados y quién aprueba el presupuesto de seguridad. Se compara luego con las decisiones del caso Uber. El material plantea la discusión, sin fijar una respuesta universal.

### RACI cotidiano

Antes de aplicarlo a ciberseguridad, se propone completar `RACI_Ejemplo_Pizza.xlsx`: compra de ingredientes, preparación de masa, decisión del tiempo de horneado y evaluación del resultado. Su propósito es practicar las diferencias entre R, A, C e I.

---

## 6. Conclusiones Clave

1. Govern define el contexto y los criterios bajo los que se decide sobre seguridad.
2. La autoridad y la rendición de cuentas deben quedar claras antes de un incidente.
3. RACI evita actividades sin dueño o con aprobaciones finales ambiguas.
4. El gobierno comprende también el riesgo de proveedores y la supervisión del programa.

## 7. Referencias del Material

* Pascoe, C., Quinn, S. y Scarfone, K. (2024). *The NIST Cybersecurity Framework (CSF) 2.0*, NIST CSWP 29.
* ISACA (2018). *COBIT 2019 Framework: Governance and Management Objectives*.
* Video de clase: cobertura del hackeo de Uber de 2016, divulgado en 2017.
