---
tags:
  - ciberseguridad
  - arquitectura
  - frameworks
  - sabsa
  - togaf
  - osa
  - obsidian
materia: Arquitectura de Ciberseguridad
unidad: 1
sesion: 2
ciclo: 6to
---

# Sesión 2: Frameworks de Arquitectura de Seguridad

> *"Sin un framework, cada arquitectura se inventa desde cero. Con un framework, se construye sobre lo ya validado."*

## 1. Objetivo de la Sesión

* Comprender los frameworks que estructuran el diseño y la gestión de la arquitectura de ciberseguridad, aplicando su lógica a un caso determinado.
* Diferenciar el propósito de **SABSA**, **OSA**, **TOGAF**, **ISO/IEC 27001-27002**, **CIS Controls**, **CSA CCM**, **NIST CSF**, **Zero Trust (NIST 800-207)** y **MITRE ATT&CK**.
* Explicar la estructura y las capas de SABSA, OSA y TOGAF como marcos de diseño.
* Elaborar una matriz SABSA simplificada y mapearla a los marcos de gestión y cumplimiento.

---

## 2. Concepto Central y Panorama

### ¿Qué es un Framework de Arquitectura de Ciberseguridad?

Es un conjunto estructurado de normas, directrices, métodos y buenas prácticas que sirve como plano o guía para diseñar, implementar y gestionar la seguridad de la información y la ciberseguridad en una organización.

```mehrmaid
graph TD
    A("<b>CÓMO PIENSA EL ARQUITECTO DE CIBERSEGURIDAD</b>") --> B("<b>NEGOCIO</b><br>Alineación al negocio")
    A --> C("<b>RIESGO</b><br>Evaluación de riesgos")
    A --> D("<b>ARQUITECTURA</b><br>Diseño y capas")
    
    B --> E("<b>DECISIONES CLAVE</b>")
    C --> E
    D --> E
    
    E --> F("<b>TECNOLOGÍA</b><br>Nube, Red, Identidad, Firewall, Datos")
    E --> G("<b>MONITOREO</b><br>Operación y mejora continua")
```

### Panorama General de Frameworks

#### Marcos de DISEÑO de Arquitectura

| Framework | ¿Qué Resuelve? | Pregunta Clave | Ejemplo Práctico |
| :--- | :--- | :--- | :--- |
| **[[#SABSA\|SABSA]]** | Traza el control al negocio y al riesgo. | ¿Qué protegemos y por qué? | Matriz What/Why/How/Who/Where/When para MFA. |
| **[[#OSA\|OSA]]** | Da un patrón de control ya validado. | ¿Ya existe una solución probada? | Patrón de autenticación fuerte para login móvil. |
| **[[#TOGAF\|TOGAF]]** | Ordena la arquitectura empresarial completa. | ¿Cómo encaja en negocio, datos, apps y tecnología? | Fase C (Aplicaciones) del ADM para app móvil. |

#### Marcos de GESTIÓN, CUMPLIMIENTO y DETECCIÓN

| Framework | ¿Qué Resuelve? | Pregunta Clave | Ejemplo Práctico |
| :--- | :--- | :--- | :--- |
| **ISO/IEC 27001-27002** | Certifica y documenta el Sistema de Gestión (SGSI). | ¿Qué control del Anexo A aplica y cómo se implementa? | Control A.8.5 (autenticación) detallado en 27002. |
| **CIS Controls** | Prioriza controles técnicos accionables por madurez. | ¿Qué controles técnicos implemento primero? | Control 6 (Gestión de Control de Acceso). |
| **CSA CCM** | Mapea controles para entornos Cloud y Multicloud. | ¿Cómo aseguro la nube? | Dominio IAM del CCM para app cloud. |
| **NIST CSF** | Organiza la gestión del riesgo cibernético. | ¿Qué función de ciberseguridad cubre? | MFA cae en la función *Protect* (Proteger). |
| **Zero Trust (NIST 800-207)** | Verifica cada acceso; nunca confía por defecto. | ¿Cómo verificamos cada solicitud de acceso? | MFA como verificación explícita en cada sesión. |
| **MITRE ATT&CK** | Cataloga tácticas y técnicas reales de atacantes. | ¿Qué técnica de ataque mitiga este control? | Mitiga T1078 (*Valid Accounts*) mediante MFA. |

---

## 3. Marcos de Diseño: TOGAF, SABSA y OSA

Ningún marco resuelve el problema completo por sí solo. Cada uno responde a una pregunta distinta en un nivel de abstracción diferente:

```mehrmaid
graph TD
    T("<b>TOGAF</b><br><i>Nivel Estratégico</i><br>¿Qué arquitectura necesita el negocio?") --> S("<b>SABSA</b><br><i>Nivel Táctico</i><br>¿Por qué necesitamos este control?")
    S --> O("<b>OSA</b><br><i>Nivel Operativo</i><br>¿Cómo lo implemento concretamente?")
```

### 3.1 TOGAF (The Open Group Architecture Framework)

* **Nivel:** Estratégico / Empresarial.
* **Metodología ADM (Architecture Development Method):** Ciclo de 8 fases iterativas.
* **4 Dominios:** Negocio, Datos, Aplicaciones y Tecnología.

```mehrmaid
graph LR
    ADM("<b>TOGAF ADM</b>") --> B("<b>Negocio</b><br>Estrategia y procesos")
    ADM --> D("<b>Datos</b><br>Estructura de información")
    ADM --> A("<b>Aplicaciones</b><br>Sistemas y servicios")
    ADM --> T("<b>Tecnología</b><br>Infraestructura, redes, nube")
```

### 3.2 SABSA (Sherwood Applied Business Security Architecture)

* **Nivel:** Táctico / Metodológico.
* Basada en el riesgo y en los objetivos del negocio.
* Método de **trazabilidad** que conecta los requisitos con la implementación.

```mehrmaid
graph TD
    C1("<b>1. Negocio (Contextual)</b><br><i>What / Why</i>: Activos y Objetivos") --> C2("<b>2. Conceptual</b><br>Principios y Políticas")
    C2 --> C3("<b>3. Lógica</b><br><i>How</i>: Servicios de Seguridad")
    C3 --> C4("<b>4. Física</b><br>Tecnologías y Mecanismos")
    C4 --> C5("<b>5. Componentes</b><br>Herramientas y Estándares")
    C5 --> C6("<b>6. Operacional</b><br>Monitoreo y Operación diaria")
```

### 3.3 OSA (Open Security Architecture)

* **Nivel:** Operativo / Técnico.
* Biblioteca abierta de patrones de arquitectura de seguridad reutilizables.
* Ofrece diagramas de referencia, límites de confianza (*Trust Boundaries*), modelos de amenazas y controles mapeados a ISO 27001 / NIST SP 800-53.

### 3.4 Comparativa de Marcos de Diseño

| Marco | Enfoque | Nivel | Entregable Típico |
| :--- | :--- | :--- | :--- |
| **TOGAF** | Arquitectura Empresarial Integral | Estratégico | Blueprints de Negocio, Datos, Apps y Tecnología |
| **SABSA** | Seguridad Basada en Riesgo de Negocio | Táctico | Perfil de Atributos de Negocio y Matriz de Trazabilidad |
| **OSA** | Patrones Técnicos Reutilizables | Operativo | Diagramas de Referencia y Controles Mapeados |

---

## 4. Marcos de Gestión, Cumplimiento y Detección

### 4.1 ISO/IEC 27001 y 27002

```mehrmaid
graph LR
    ISO27001("<b>ISO/IEC 27001</b><br>Certifica el SGSI (Ciclo PDCA)") --> ISO27002("<b>ISO/IEC 27002</b><br>93 Controles de Ciberseguridad")
    
    ISO27002 --> C1("<b>Organizacionales</b><br>(37 controles)")
    ISO27002 --> C2("<b>Personas</b><br>(8 controles)")
    ISO27002 --> C3("<b>Físicos</b><br>(14 controles)")
    ISO27002 --> C4("<b>Tecnológicos</b><br>(34 controles)")
```

### 4.2 CIS Controls (Center for Internet Security)

Organizados en 3 **Grupos de Implementación (IG)**:

* **IG1 (Higiene Básica):** 56 salvaguardas (organizaciones esenciales sin equipo dedicado).
* **IG2 (Gestión de Riesgo):** +74 salvaguardas (equipos de TI dedicados).
* **IG3 (Alta Madurez):** +23 salvaguardas (especialistas en ciberseguridad y activos críticos).

### 4.3 CSA CCM (Cloud Controls Matrix)

Marco de controles específico para entornos Cloud y Multicloud (17 dominios, incluyendo IAM, Seguridad de Datos, APIs, Gobernanza y Gestión de Amenazas).

### 4.4 NIST Cybersecurity Framework (NIST CSF 2.0)

```mehrmaid
graph LR
    NIST("<b>NIST CSF 2.0</b>") --> G("<b>Govern</b><br>Gobernar")
    NIST --> I("<b>Identify</b><br>Identificar")
    NIST --> P("<b>Protect</b><br>Proteger")
    NIST --> D("<b>Detect</b><br>Detectar")
    NIST --> R("<b>Respond</b><br>Responder")
    NIST --> RC("<b>Recover</b><br>Recuperar")
```

### 4.5 Zero Trust Architecture (NIST SP 800-207)

Modelo basado en el principio: *"Nunca confiar, siempre verificar"*.

### 4.6 MITRE ATT&CK

Matriz de conocimiento de tácticas y técnicas de atacantes reales para equipos de ciberdefensa.

---

## 5. De la Metodología al Diseño: Los 14 Pasos

```mehrmaid
graph TD
    P1("<b>1. Contexto Empresarial</b>") --> P2("<b>2. Objetivos de Seguridad</b>")
    P2 --> P3("<b>3. Activos y Procesos Críticos</b>")
    P3 --> P4("<b>4. Amenazas y Riesgos</b>")
    P4 --> P5("<b>5. Requisitos de Seguridad</b>")
    P5 --> P6("<b>6. Principios de Arquitectura</b>")
    P6 --> P7("<b>7. Capacidades de Seguridad</b>")
    P7 --> P8("<b>8. Dominios de Seguridad</b>")
    P8 --> P9("<b>9. Arquitectura Conceptual</b>")
    P9 --> P10("<b>10. Arquitectura Lógica</b>")
    P10 --> P11("<b>11. Patrones OSA Aplicables</b>")
    P11 --> P12("<b>12. Controles NIST / ISO / CIS</b>")
    P12 --> P13("<b>13. Arquitectura Física / Tecnológica</b>")
    P13 --> P14("<b>14. Roadmap de Implementación</b>")
```

### Ejemplo de Arquitectura Lógica Zero Trust

```mehrmaid
graph TD
    U("<b>USUARIOS</b>") --> ID("<b>IDENTIDAD</b><br>Autenticación, MFA / SSO")
    ID --> DP("<b>DEVICE POSTURE</b><br>Evaluación de Estado de Dispositivo")
    DP --> AC("<b>ACCESS CONTROL</b><br>Decisión de Políticas (Policy Engine)")
    AC --> AD("<b>APLICACIONES / DATOS</b><br>Acceso Restringido")
    
    ID -.-> SM("<b>SECURITY MONITORING</b><br>SIEM / SOAR")
    DP -.-> SM
    AC -.-> SM
    AD -.-> SM
```

---

## 6. Caso Práctico: Andina Salud (Red de Clínicas)

### Contexto
Red de clínicas privadas (800 colaboradores, 6 clínicas, portal de telemedicina) que digitalizó su Historia Clínica Electrónica (HCE). Sufrió incidentes de acceso indebido por credenciales compartidas.

### Matriz SABSA - Capa Contextual (Negocio)

| Pregunta | Respuesta (HCE - Andina Salud) | Justificación |
| :--- | :--- | :--- |
| **What** | Historia Clínica Electrónica (HCE) y portal de telemedicina. | Contiene datos sensibles de salud de los pacientes. |
| **Why** | Evitar accesos indebidos, sanciones por Ley N° 29733 y pérdida de reputación. | Un incidente afecta la continuidad operativa y la confianza. |
| **How** | Control de acceso basado en roles (RBAC) + MFA. | Mitiga el uso de credenciales compartidas. |
| **Who** | Comité de TI y Seguridad + Jefe de Sistemas Clínicos (dueño). | Centraliza decisiones de seguridad entre sedes. |
| **Where** | Data Center del proveedor cloud y las 6 sedes clínicas. | Estandariza el control en todos los puntos de acceso. |
| **When** | Revisión trimestral de accesos y MFA activo permanentemente. | Previene accesos no autorizados por rotación de personal. |

---

## 7. Conclusiones Clave

1. **Un framework no diseña por ti:** Estructura las preguntas necesarias para que el diseño sea trazable y justificado hacia el negocio.
2. **Complementariedad:**
   * **SABSA:** Define el *Qué* y el *Por qué* (negocio/riesgo).
   * **TOGAF:** Sitúa la seguridad dentro de la arquitectura empresarial.
   * **OSA:** Proporciona el *Cómo* mediante patrones técnicos.
   * **ISO / CIS / CSA:** Implementan y aseguran cumplimiento.
   * **NIST CSF / Zero Trust / MITRE:** Gestionan, verifican y detectan amenazas.
3. **Juicio Experto:** El Arquitecto de Ciberseguridad conecta todas estas metodologías aplicando su criterio según el contexto real de la organización.