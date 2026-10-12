---
tags:
  - ciberseguridad
  - procesos
  - activos
  - riesgos
  - nist_csf
materia: Procesos de Ciberseguridad
unidad: 1
sesion: 3
ciclo: 6to
diapositivas: 34
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546139_1/file/_75752165_1?courseId=_546139_1
---

# Sesión 3: Identify, Activos, Riesgos y Perfil de Madurez

## 1. Objetivo de la Sesión

* Reconocer activos, contexto y dependencias del negocio.
* Aplicar ID.AM, ID.RA e ID.IM del NIST CSF 2.0.
* Distinguir amenaza, vulnerabilidad, probabilidad e impacto.
* Clasificar y valorar activos y construir un Current Profile.

---

## 2. Repaso: Estructura de una Política de Seguridad

La política de la categoría **GV.PO**, estudiada en [[Govern y Gobierno de Ciberseguridad|Govern]], debe precisar:

| Elemento | Pregunta |
| :--- | :--- |
| Propósito | ¿Por qué existe? |
| Alcance | ¿A quién y a qué aplica? |
| Responsables | ¿Quién la hace cumplir? |
| Cumplimiento | ¿Qué ocurre si no se sigue? |

El ejemplo del material es una política de contraseñas para proteger cuentas de empleados y contratistas, con responsables TI/CISO y bloqueo tras tres intentos fallidos. Es un ejemplo académico, no una configuración obligatoria para cualquier sistema. Las diapositivas repiten esta sección y utilizan el rótulo GO.PO; se normaliza aquí como GV.PO.

---

## 3. Caso de Clase: Equifax (2017)

La presentación describe una brecha que afectó a **147 millones de personas** y relaciona el incidente con una vulnerabilidad conocida de Apache Struts que no se corrigió a tiempo.

El caso permite analizar inventario, visibilidad, gestión de parches y priorización. Conocer una vulnerabilidad resulta insuficiente si no se identifican los sistemas afectados, no se asigna responsabilidad y no se ejecuta el tratamiento del riesgo.

---

## 4. Función Identify

Identify construye el mapa de activos, riesgos y dependencias. Su punto de partida es conocer qué existe y qué valor tiene para el negocio.

| Código | Categoría | Función |
| :--- | :--- | :--- |
| ID.AM | Gestión de activos | Inventario de hardware, software, datos y sistemas externos |
| ID.RA | Evaluación de riesgos | Amenazas, vulnerabilidades, probabilidad e impacto |
| ID.IM | Mejora continua | Aprendizaje desde evaluaciones, auditorías e incidentes |

El análisis incluye el contexto de negocio y las dependencias: qué sistemas necesitan a otros y qué consecuencias tendría su falla.

---

## 5. ID.AM: Gestión de Activos

### 5.1 Categorías del inventario

| Tipo | Ejemplos |
| :--- | :--- |
| Hardware | Laptops, servidores y celulares corporativos |
| Software | Sistemas operativos, aplicaciones y bases de datos |
| Datos | Información de clientes, finanzas y RR. HH. |
| Personas | Empleados, contratistas y administradores |
| Proveedores / terceros | Nube, mantenimiento y consultoría |

Un inventario completo incluye las cinco categorías. Para cada activo se identifica **qué es, quién es su propietario y dónde se encuentra o resguarda**.

### 5.2 Proceso de gestión

1. Identificar o actualizar activos de los procesos.
2. Definir el dueño de cada activo.
3. Clasificar sus necesidades de confidencialidad, integridad y disponibilidad.
4. Asignar un valor final mediante los criterios definidos.
5. Documentar clasificación y valoración en el inventario.
6. Difundir el inventario a los responsables que necesitan utilizarlo.

### 5.3 Técnicas para identificar activos

* **Talleres:** explicar objetivos y pasos a los participantes de los procesos.
* **Cuestionarios:** preguntar por entradas y salidas de los procesos.
* **Reuniones:** recorrer el proceso con sus responsables e identificar activos y posibles riesgos.
* **Revisión documental:** estudiar manuales y procesos antes del levantamiento.

### 5.4 Clasificación CID

| Criterio | Necesidad | Niveles usados en el ejercicio |
| :--- | :--- | :--- |
| Confidencialidad | Acceso limitado a quienes están autorizados | Público, uso interno, confidencial |
| Integridad | Datos auténticos, precisos y sin alteraciones indebidas | Baja, media, alta |
| Disponibilidad | Acceso a datos y servicios cuando se necesitan | Baja, media, alta |

### 5.5 Valoración: tabla gráfica del docente

| Criterio | Puntaje 5 | Puntaje 3 | Puntaje 1 |
| :--- | :--- | :--- | :--- |
| Confidencialidad | Confidencial | Uso interno | Público |
| Integridad | Alta | Media | Baja |
| Disponibilidad | Alta | Media | Baja |

El ejemplo suma las puntuaciones CID:

| Activo | Confidencialidad | Integridad | Disponibilidad | Resultado |
| :--- | ---: | ---: | ---: | ---: |
| Estados financieros | 1 | 5 | 5 | 11 |
| Estrategia de marketing | 5 | 5 | 3 | 13 |
| Gantt de proyecto | 3 | 3 | 1 | 7 |

Se conserva la clasificación que muestra la diapositiva. Los valores son ilustrativos y dependen del contexto, alcance y criterios aprobados por la organización.

---

## 6. ID.RA: Evaluación de Riesgos

### 6.1 Amenaza y vulnerabilidad

| Concepto | Definición | Ejemplos del material |
| :--- | :--- | :--- |
| Amenaza | Evento, persona o circunstancia con potencial de daño | Atacante, ransomware, phishing, error humano, incendio o inundación |
| Vulnerabilidad | Debilidad de sistema, proceso o persona que una amenaza puede aprovechar | Falta de parches, contraseña débil, personal sin formación, falta de segmentación o de respuesta |

El material resume la aparición de riesgo como **amenaza y vulnerabilidad coincidentes**. La analogía compara una puerta sin llave con la existencia de un ladrón. Este esquema conceptual explica el escenario de riesgo; la valoración posterior utiliza probabilidad e impacto.

### 6.2 Probabilidad

Es la posibilidad de que una amenaza explote una vulnerabilidad en un periodo definido. Puede expresarse en muy baja, baja, media, alta o muy alta. Depende de exposición, actividad de la amenaza y controles existentes.

Un sistema vulnerable expuesto a Internet suele tener mayor exposición que uno accesible únicamente desde una red interna controlada.

### 6.3 Impacto

Describe las consecuencias para la organización cuando un riesgo se materializa:

* Costos directos: multas, remediación e indemnizaciones.
* Costos indirectos: pérdida de ventas, clientes o tiempo de operación.
* Daño reputacional: efectos sobre confianza y relaciones a largo plazo.

Como ejemplos, las diapositivas citan más de 300 millones de dólares para Target y hasta 700 millones para Equifax. Son cifras de los casos presentados por el docente.

### 6.4 Fórmula y matriz

$$\text{Nivel de riesgo} = \text{Probabilidad} \times \text{Impacto}$$

La matriz combina cinco niveles de probabilidad con cinco niveles de impacto y utiliza categorías bajo, medio, alto y crítico. Su finalidad es priorizar atención y tratamiento.

El ejemplo del docente ubica un sistema crítico vulnerable y expuesto a Internet con probabilidad alta e impacto alto, y lo clasifica como riesgo alto que requiere pronta atención. El resultado concreto debe seguir la matriz que adopte cada organización.

### 6.5 Actividades de clase

**Distinguir amenaza y vulnerabilidad:** exempleado con acceso activo, servidor desactualizado, huracán, contraseñas en un papel, grupo de ransomware y falta de backups.

**Ubicar riesgos en la matriz:** contraseña reutilizada, servidor crítico sin backup en zona sísmica, aplicación interna sin parchar y base de datos de clientes sin cifrado expuesta a Internet. El ejercicio requiere estimar probabilidad e impacto y justificar la valoración.

---

## 7. ID.IM y Current Profile

ID.IM utiliza auditorías, evaluaciones, pruebas e incidentes para identificar mejoras. La pregunta central es qué aprendió la organización y qué cambió a partir de ese aprendizaje.

El **Current Profile** describe el estado actual de los resultados. La presentación propone valorar la gestión de Equifax antes del incidente usando los niveles parcial, riesgo informado, repetible y adaptativo, vistos en la [[Ciberseguridad como proceso de negocio y NIST CSF 2.0|Sesión 1]]. El aprendizaje y las brechas alimentan el Target Profile y el roadmap.

La sesión 4 corresponde a la PC1 sobre las sesiones 1 a 3 y a la presentación de una organización real con un incidente documentado entre 2019 y 2025.

## 8. Conclusiones Clave

1. El inventario debe abarcar activos técnicos y organizacionales, con propietarios y ubicación.
2. Clasificación y valoración CID ayudan a priorizar activos.
3. Probabilidad e impacto permiten comparar escenarios de riesgo.
4. Current Profile, aprendizaje y Target Profile conectan diagnóstico con mejora.

## 9. Referencias del Material

* Pascoe, C., Quinn, S. y Scarfone, K. (2024). *The NIST Cybersecurity Framework (CSF) 2.0*, NIST CSWP 29.
* ISO/IEC 27001:2022 e ISO/IEC 27002:2022.
* Splunk. *Vulnerabilities, Threats & Risk Explained*.
* Video de clase: *Equifax Data Breach Explained*.
