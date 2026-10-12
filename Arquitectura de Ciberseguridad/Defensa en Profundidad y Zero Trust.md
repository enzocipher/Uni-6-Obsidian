---
tags:
  - ciberseguridad
  - arquitectura
  - defensa_en_profundidad
  - zero_trust
  - nist_800_207
materia: Arquitectura de Ciberseguridad
unidad: 1
sesion: 4
ciclo: 6to
---

# Sesión 4: Defensa en Profundidad y Zero Trust

> *"Never trust, always verify."*

## 1. Objetivo de la Sesión

* Aplicar defensa en profundidad, mínimo privilegio y denegación por defecto al diseño arquitectónico.
* Describir los principios y componentes de Zero Trust según NIST SP 800-207.
* Comparar la seguridad perimetral tradicional con la verificación por solicitud.
* Evaluar una arquitectura e identificar cómo limitar el impacto de una brecha.

---

## 2. Principios de Diseño Seguro

### 2.1 Defensa en profundidad

Ningún control es perfecto. La defensa en profundidad despliega controles redundantes y complementarios en distintos niveles para que, si una capa falla, las demás contengan el avance del atacante. Las capas pueden incluir perímetro, red, host, aplicación y datos. El objetivo final es proteger el activo, no solo el borde de la red.

### 2.2 Mínimo privilegio (*least privilege*)

Cada usuario, servicio o proceso debe operar con los permisos estrictamente necesarios para cumplir su función. En la arquitectura esto se traduce en roles granulares (RBAC o ABAC), credenciales de duración limitada y segmentación que reduzca el radio de impacto.

**Ejemplo:** un desarrollador que necesita consultar los registros de un microservicio de producción recibe un rol de solo lectura, limitado a ese servicio y con vencimiento definido, en lugar de permisos de administrador del clúster.

### 2.3 Denegación por defecto (*fail-safe defaults*)

Ante un fallo o una situación no contemplada, el sistema debe adoptar el estado más seguro: denegar el acceso. Se permite únicamente lo autorizado por una regla explícita. Así, un error de configuración no abre involuntariamente el acceso.

### 2.4 Principios complementarios

| Principio | Decisión de diseño | Efecto |
| :--- | :--- | :--- |
| Defensa en profundidad | Aplicar controles en varias capas | Contiene el avance si una capa falla |
| Mínimo privilegio | Limitar permisos por identidad, recurso y tiempo | Reduce exposición y abuso de privilegios |
| Denegación por defecto | Permitir solo lo definido explícitamente | Evita accesos abiertos por omisión |

---

## 3. Modelo Zero Trust

### 3.1 Concepto

Zero Trust sustituye la confianza implícita basada en la ubicación por la verificación explícita de cada solicitud, tanto si se origina dentro como fuera de la red corporativa. El modelo responde a entornos donde aplicaciones, usuarios y dispositivos están distribuidos entre nube, sedes, trabajo remoto y terceros.

### 3.2 Principios centrales

1. **Verificación explícita:** autenticar y autorizar cada solicitud según identidad, dispositivo, ubicación y comportamiento.
2. **Mínimo privilegio:** conceder solo el acceso necesario, por el tiempo necesario y con revisión continua.
3. **Asumir la brecha:** diseñar como si un atacante pudiera estar ya dentro; segmentar y monitorear para limitar el impacto.

### 3.3 Componentes de referencia

| Componente | Función |
| :--- | :--- |
| Sujeto | Usuario, dispositivo o servicio que solicita acceso |
| Policy Decision Point (PDP) | Evalúa si la solicitud cumple la política y el contexto |
| Policy Enforcement Point (PEP) | Permite, bloquea o monitorea la conexión según la decisión |
| Recurso | Aplicación, dato o sistema al que se solicita acceso |

Cada solicitud pasa por un punto de aplicación que consulta la decisión de política. La ubicación de red por sí sola no otorga confianza y la decisión puede reevaluarse durante la sesión.

### 3.4 Perímetro tradicional y Zero Trust

| Criterio | Perimetral tradicional | Zero Trust |
| :--- | :--- | :--- |
| Supuesto base | Lo interno es confiable | Ninguna conexión es confiable por defecto |
| Control principal | Firewall en el borde | Verificación de cada solicitud |
| Identidad | Se verifica al ingresar a la red | Se evalúa explícitamente al acceder al recurso |
| Segmentación | Red plana o zonas amplias | Segmentación por recurso o zona |
| Brecha | Puede facilitar movimiento lateral | La segmentación limita el radio de impacto |
| Nube y acceso remoto | Depende de una red corporativa definida | No depende de la ubicación física |

Zero Trust no elimina automáticamente firewalls, VPN ni controles en capas; cambia el criterio de confianza y exige control por recurso, identidad y contexto.

---

## 4. Del Riesgo al Diseño

El arquitecto conecta los objetivos de negocio con controles justificables mediante un ciclo iterativo:

1. Entender el negocio, sus procesos críticos y su apetito de riesgo.
2. Identificar activos, amenazas y vulnerabilidades, retomando la gestión de riesgos de la [[Gestión de riesgos en arquitectura de seguridad|Sesión 3]].
3. Definir requisitos de defensa en profundidad, mínimo privilegio y Zero Trust.
4. Seleccionar controles y patrones apoyándose en marcos como SABSA, OSA, NIST y CIS.
5. Diagramar, revisar y documentar la arquitectura; repetir el análisis cuando cambien los riesgos o el negocio.

### Ejemplo de trazabilidad

| Elemento | Banca móvil |
| :--- | :--- |
| Objetivo de negocio | Ofrecer banca móvil disponible desde redes no confiables |
| Riesgo | Acceso indebido a cuentas desde dispositivos comprometidos |
| Apetito de riesgo | Averso al fraude transaccional |
| Requisito | Verificar explícitamente cada acceso, sin importar su origen |
| Componentes | PEP y PDP delante de cada servicio, con monitoreo continuo |

### Arquitectura de referencia resumida

Usuarios remotos, dispositivos corporativos y socios externos aportan señales de identidad, MFA, postura y comportamiento. Un PEP aplica la decisión del PDP antes de permitir acceso a aplicaciones críticas, datos sensibles o servicios internos segmentados. El monitoreo (SOC/SIEM) retroalimenta la evaluación del riesgo.

---

## 5. Caso de Clase: Banco Altiplano Digital

El caso describe empleados conectados a la red corporativa con acceso directo a un servidor central de transacciones. Tras reportarse una laptop comprometida por malware, la arquitectura debe evaluarse frente a estos principios:

* **Defensa en profundidad:** añadir controles entre la red de usuarios y las transacciones.
* **Mínimo privilegio:** restringir el acceso a los servicios y operaciones requeridos por cada rol.
* **Zero Trust:** verificar identidad, estado del dispositivo y contexto en cada solicitud.
* **Contención:** segmentar la red y monitorear para impedir que un equipo comprometido alcance todos los recursos.

La actividad del material propone discutir qué principios se incumplen, qué cambios aplicar y cómo reducir el radio de impacto.

---

## 6. Conclusiones Clave

1. La defensa en profundidad distribuye controles y limita el avance cuando una capa falla.
2. El mínimo privilegio y la denegación por defecto reducen el acceso innecesario y los errores permisivos.
3. Zero Trust verifica cada solicitud y no confía en una conexión solo por su ubicación.
4. Los principios deben convertirse en requisitos y controles trazables a riesgos reales.

## 7. Referencias

* NIST SP 800-207, *Zero Trust Architecture*.
* ISO/IEC 27001:2022, *Information Security Management Systems — Requirements*.
* Sherwood, Clark y Lynas, *Enterprise Security Architecture* (SABSA).
* NIST Cybersecurity Framework (CSF) 2.0.
