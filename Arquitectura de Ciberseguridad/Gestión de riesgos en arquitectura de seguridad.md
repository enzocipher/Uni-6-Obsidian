---
tags:
  - ciberseguridad
  - arquitectura
  - gestion_de_riesgos
  - iso27005
  - nist_rmf
materia: Arquitectura de Ciberseguridad
unidad: 1
sesion: 3
ciclo: 6to
---

# Sesión 3: Gestión de Riesgos como Base del Diseño Arquitectónico

> *"El riesgo que no se mide, se hereda como deuda técnica de seguridad."*

---

## 1. Objetivo de la Sesión

* **Aplicar** metodologías de análisis de riesgo (**ISO/IEC 27005** y **NIST RMF**) para identificar activos, amenazas y vulnerabilidades.
* **Traducir** el apetito de riesgo organizacional en requisitos de arquitectura de seguridad concretos, medibles y justificables.
* **Diferenciar** entre riesgo inherente y residual, y calcular el nivel de riesgo de un activo.
* **Elaborar** una matriz de riesgos integral y derivar de ella capacidades de arquitectura.

---

## 2. Bloque 1: Fundamentos de Gestión de Riesgo

### Concepto Central
La gestión de riesgos en la arquitectura de seguridad **no es un checklist de controles**: es el criterio que justifica por qué se elige un control y no otro. Conecta el riesgo de negocio con la capa lógica y de componentes ([[Frameworks de arquitectura de seguridad#3.2 SABSA (Sherwood Applied Business Security Architecture)|SABSA]]) del entorno tecnológico.

### Definiciones Clave
1. **Activo:** Todo aquello que tiene valor para la organización y debe protegerse (datos, sistemas, procesos, personas, reputación).
2. **Amenaza:** Cualquier evento u actor con potencial de causar daño a un activo (atacante, error humano, desastre natural).
3. **Vulnerabilidad:** Una debilidad en un activo o control que una amenaza puede explotar (falta de parches, mala configuración, ausencia de MFA).

### La Ecuación del Riesgo

$$\text{Riesgo} = \text{Probabilidad} \times \text{Impacto}$$

```mehrmaid
graph LR
    A("<b>Activo</b><br>¿Qué protegemos?") --- B("<b>Amenaza</b><br>¿Quién/Qué puede dañarlo?")
    B --- C("<b>Vulnerabilidad</b><br>¿Por dónde puede entrar?")
    C --> R("<b>RIESGO RESULTANTE</b><br><i>Probabilidad x Impacto</i>")
```

> **Regla de Oro:** Sin activo no hay nada que proteger. Sin amenaza y vulnerabilidad no hay riesgo real, solo exposición teórica.

### Proceso de Análisis y Gestión del Riesgo

```mehrmaid
graph TD
    subgraph F1["FASE 01: Alcance e Inventario"]
        A1("Establecer alcance de la Gestión del Riesgo") --> A2("Inventario de Activos por proceso")
        A2 --> A3("Asignación de propietarios de activos")
        A3 --> A4("Valoración de activos (CIA: C, I, A)")
    end

    subgraph F2["FASE 02: Evaluación y Criterios"]
        B1("Detección de Amenazas y Vulnerabilidades") --> B2("Evaluación del Riesgo")
        B2 --> B3("Aplicación de criterios de aceptación aprobados")
        B3 --> B4("Asignación de propietarios de los riesgos")
    end

    subgraph F3["FASE 03: Tratamiento y Residual"]
        C1("Elaboración del Plan de Tratamiento") --> C2("Evaluación del Riesgo Residual")
    end

    F1 --> F2
    F2 --> F3
```

### Panorama de Fuentes de Amenaza

| Origen | Descripción | Ejemplo Típico |
| :--- | :--- | :--- |
| **Interna** | Colaboradores, contratistas o procesos internos (intencional o no). | Empleado que exfiltra datos o comparte credenciales. |
| **Externa** | Actores maliciosos que buscan explotar el entorno deliberadamente. | Ransomware, phishing, explotación de APIs expuestas. |
| **Tecnológica / Accidental** | Fallas técnicas, errores de configuración o de software. | Caída de un servidor, parche mal aplicado, bug en producción. |
| **Ambiental / Natural** | Eventos físicos que afectan la infraestructura. | Corte eléctrico, inundación, sismo en el data center. |
| **Cadena de Suministro** | Riesgo heredado de proveedores o socios integrados. | Brecha en un proveedor cloud o API de un partner fintech. |

---

## 3. Bloque 2: Metodologías de Análisis de Riesgo

```mehrmaid
graph TD
    M("<b>Metodologías de Riesgo</b>") --> ISO("<b>ISO/IEC 27005</b><br><i>Cíclico y Flexible</i><br>Alineado a ISO 27001 (SGSI)")
    M --> NIST("<b>NIST RMF</b><br><i>7 Pasos Secuenciales</i><br>Requiere Autorización Formal (ATO)")
    
    ISO --> OUT1["Plan de Tratamiento de Riesgos"]
    NIST --> OUT2["Autorización de Operación (ATO)"]
```

### 3.1 ISO/IEC 27005 (Ciclo Integrado)

```mehrmaid
graph LR
    P1("<b>1. Contexto</b><br>Alcance y criterios") --> P2("<b>2. Valoración</b><br>Identificación y análisis")
    P2 --> P3("<b>3. Tratamiento</b><br>Mitigar, transferir, evitar, aceptar")
    P3 --> P4("<b>4. Aceptación</b><br>Decisión del dueño del riesgo")
    P4 --> P5("<b>5. Monitoreo</b><br>Revisión continua")
    P5 --> P1
```

### 3.2 NIST RMF (Risk Management Framework - 7 Pasos)

```mehrmaid
graph LR
    S1("<b>1. Prepare</b><br>Roles y estrategia") --> S2("<b>2. Categorize</b><br>Clasificar sistema")
    S2 --> S3("<b>3. Select</b><br>Seleccionar controles")
    S3 --> S4("<b>4. Implement</b><br>Implementar controles")
    S4 --> S5("<b>5. Assess</b><br>Evaluar efectividad")
    S5 --> S6("<b>6. Authorize</b><br>Autorizar operación (ATO)")
    S6 --> S7("<b>7. Monitor</b><br>Monitoreo continuo")
```

### 3.3 Comparación Rápida: ISO/IEC 27005 vs. NIST RMF

| Criterio | ISO/IEC 27005 | NIST RMF |
| :--- | :--- | :--- |
| **Origen** | ISO (Internacional). | NIST (Gobierno EE. UU.). |
| **Enfoque** | Cíclico, cuantitativo/cualitativo, flexible. | Secuencial, de autorización formal (*Compliance*). |
| **Alineación Natural** | ISO/IEC 27001 (SGSI). | FISMA, NIST CSF, SP 800-53. |
| **Entregable Clave** | Plan de Tratamiento del Riesgo. | Autorización de Operación (ATO - *Authority to Operate*). |

### 3.4 Riesgo Inherente vs. Riesgo Residual

* **Riesgo Inherente:** Exposición en "crudo", sin controles compensatorios aplicados.
* **Controles Aplicados:** Reducen la probabilidad, el impacto o ambos (nunca eliminan el riesgo al 100%).
* **Riesgo Residual:** El nivel de riesgo final que la organización asume y que debe contrastarse contra el **Apetito de Riesgo**.

---

## 4. Bloque 3: Del Negocio a la Arquitectura (Apetito de Riesgo)

El **Apetito de Riesgo** es el nivel y tipo de riesgo que una organización está dispuesta a aceptar en la búsqueda de sus objetivos de negocio. **Lo define la alta dirección, no el área de TI/Ciberseguridad.**

```mehrmaid
graph TD
    A1("<b>1. Averso (Conservador)</b><br>Minimiza exposición.<br><i>Banca, Salud, Sector Público</i>") --- A2("<b>2. Neutral / Equilibrado</b><br>Balancea riesgo/oportunidad.<br><i>Retail, Manufactura</i>")
    A2 --- A3("<b>3. Buscador de Riesgo</b><br>Prioriza velocidad e innovación.<br><i>Startups Early-Stage</i>")
```

### Trazabilidad de Decisión de Riesgo

```mehrmaid
graph LR
    R["<b>Riesgo Identificado</b><br>Activo + Amenaza + Vuln."] --> AP["<b>Apetito de Riesgo</b><br>¿Es aceptable para el negocio?"]
    AP --> REQ["<b>Requisito de Seguridad</b><br>Qué debe garantizar la arquitectura"]
    REQ --> CAP["<b>Capacidad / Control</b><br>Cómo se materializa (SABSA / OSA)"]
```

### Caso de Estudio Ampliado: Analogía de los Dos Filtros (Defensa en Profundidad)

Para mitigar riesgos de APIs expuestas a terceros, no basta un solo control. Se implementa una estrategia Zero Trust:

```mehrmaid
graph TD
    subgraph F1["Filtro 1: Puerta Principal (Identidad)"]
        A["Cliente Tercero"] -- "mTLS (Autenticación Mutua)" --> B["API Gateway"]
    end

    subgraph F2["Filtro 2: Pasillo Interno (Permisos / Contexto)"]
        B -- "Validar Token OAuth 2.0 + Scopes" --> C{"Scope Válido?"}
        C -- "Sí" --> D["Servicio / Base de Datos"]
        C -- "No" --> E["Acceso Denegado (403)"]
    end
```

* **mTLS (Filtro 1):** Garantiza la identidad mutua entre cliente y servidor. *(Previene impersonación de red)*.
* **OAuth 2.0 + Scopes (Filtro 2):** Delimita estrictamente a qué recursos/operaciones tiene permiso de acceder esa identidad. *(Previene movimiento lateral y elevación de privilegios)*.

---

## 5. Bloque 4: Integración del Riesgo con Frameworks de Arquitectura

La gestión de riesgos pone en marcha los frameworks de arquitectura vistos en la [[Frameworks de arquitectura de seguridad|Sesión 2]]:

```mehrmaid
graph TD
    OBJ("<b>Objetivo de Negocio</b>") --> RIE("<b>Riesgo (Activo + Amenaza)</b>")
    RIE --> APE("<b>Apetito de Riesgo</b>")
    APE --> SAB("<b>Requisito de Arquitectura (SABSA)</b>")
    SAB --> TEC("<b>Control Técnico (OSA / CIS Controls / NIST 800-53 / OWASP)</b>")
```

| Framework | ¿Dónde entra el análisis de riesgo? | Entregable / Resultado |
| :--- | :--- | :--- |
| **SABSA** | Capa Contextual (*What / Why*). | Atributos de seguridad justificados por riesgo. |
| **TOGAF (ADM)** | Fase B: Arquitectura de Negocio. | Requisitos de seguridad integrados al ciclo ADM. |
| **OSA** | Selección de Patrones Técnicos. | Patrones aplicados según la severidad del riesgo. |
| **ISO/IEC 27001** | Análisis de Riesgo según ISO 27005. | Declaración de Aplicabilidad (SoA) justificada. |
| **NIST CSF 2.0** | Función *Identify* (Identificar). | Perfil de ciberseguridad priorizado por impacto. |

---

## 6. Caso Práctico Guiado: Andina Retail

### Contexto del Caso
* **Giro:** Cadena de retail (40 tiendas físicas + E-commerce + App móvil).
* **Sensibilidad:** Procesa tarjetas de crédito/débito (Cumplimiento PCI DSS).
* **Incidente Reciente:** Intento de acceso no autorizado a la base de datos de clientes desde la red WiFi de una tienda física.

### Matriz de Riesgos y Requisitos Derivados

| Activo | Amenaza | Vulnerabilidad | Nivel de Riesgo | Requisito de Arquitectura | Capacidad / Framework |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **E-commerce (Datos de Tarjetas)** | Inyección SQL / Exfiltración externa. | Falta de validación de entradas; ausencia de tokenización. | **Alto** ($\text{Alta} \times \text{Alto}$) | Implementación de WAF, validación estricta en pipeline DevSecOps y tokenización de tarjetas. | SABSA Lógica / CIS Control 16 / PCI DSS. |
| **POS en Tiendas** | Malware especializado en captura de memoria (RAM Scraping). | Red de pagos compartida con la red general de la tienda. | **Alto** ($\text{Media} \times \text{Alto}$) | Segmentación física/lógica de la red de pagos y whitelisting de aplicaciones en POS. | SABSA Física / CIS Control 10. |
| **Red WiFi de Tiendas** | Acceso indebido a la BD de clientes. | Red WiFi de invitados sin aislamiento de la LAN interna. | **Alto** ($\text{Alta} \times \text{Alto}$) | Segmentación estricta por VLANs independientes y Control de Acceso a la Red (NAC). | SABSA Física / Zero Trust Architecture. |
| **ERP de Inventario** | Indisponibilidad por sobrecarga en fechas pico (Cyber Days). | Infraestructura monolítica sin escalamiento automático. | **Medio** ($\text{Media} \times \text{Medio}$) | Arquitectura de alta disponibilidad con balanceo de carga y redundancia geográfica. | SABSA Componentes / NIST CSF (*Recover*). |

---

## 7. Conclusiones y Puntos Clave

1. **El riesgo se mide sobre activos:** Sin la triada **Activo - Amenaza - Vulnerabilidad**, no existe un análisis de riesgo real.
2. **Metodologías complementarias:** ISO 27005 estructura la gestión continua del riesgo (SGSI); NIST RMF proporciona una guía rigurosa de autorización operativa.
3. **Traducción estratégica:** El negocio define la tolerancia (Apetito); el arquitecto traduce esa tolerancia en **controles lógicos, físicos y componentes de software**.
4. **Trazabilidad total:** Cada firewall, API Gateway, regla de cifrado o política de autenticación debe estar vinculado directamente a un riesgo que busque mitigar.
