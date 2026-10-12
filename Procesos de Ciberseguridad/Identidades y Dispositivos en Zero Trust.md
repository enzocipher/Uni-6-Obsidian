---
tags:
  - ciberseguridad
  - procesos
  - zero_trust
  - identidad
  - dispositivos
  - iam
  - edr
materia: Procesos de Ciberseguridad
unidad: 2
sesion: 6
ciclo: 6to
diapositivas: 35
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546139_1/file/_75964537_1?courseId=_546139_1
---

# Sesión 6: Identidades y Dispositivos en Zero Trust

## 1. Objetivo de la Sesión

* Profundizar en los siete principios formales de NIST SP 800-207.
* Distinguir los pilares del modelo CISA y los dominios de trabajo del curso.
* Diseñar procesos y controles para identidades y dispositivos.
* Aplicar Protect, Detect, Respond y Recover a ambos dominios.

La sesión desarrolla los principios introducidos en [[Zero Trust, Concepto y Principios|la sesión 5]] y conecta la seguridad con procesos de autenticación, soporte, gestión de permisos y control de endpoints.

---

## 2. Caso de Clase: MGM Resorts (2023)

El material describe una llamada de ingeniería social del grupo Scattered Spider a la mesa de ayuda. Mediante información de un empleado obtenida en LinkedIn, el atacante consiguió el restablecimiento de MFA de una cuenta privilegiada.

La pregunta de clase es qué falla si la autenticación se elude a través del proceso de recuperación sin explotar una vulnerabilidad técnica. El análisis enfatiza que la recuperación de cuentas necesita una verificación tan cuidadosa como el acceso normal.

---

## 3. Siete Principios Formales de NIST SP 800-207

Los tres principios prácticos de Microsoft resumen Zero Trust. NIST SP 800-207 desarrolla siete principios (*tenets*) más específicos:

| N.º | Principio formal resumido | Ejemplo del material | Síntesis práctica relacionada |
| :--- | :--- | :--- | :--- |
| 1 | Todas las fuentes de datos y servicios de cómputo se consideran recursos | IoT, BYOD y procesos temporales cloud también se protegen | Verify Explicitly |
| 2 | Toda comunicación se asegura sin importar ubicación | Cifrar y autenticar también entre servidores del mismo datacenter | Verify Explicitly |
| 3 | El acceso se concede por sesión | Acceder inicialmente no otorga permisos permanentes a todos los recursos | Least Privilege |
| 4 | La política es dinámica y considera identidad, dispositivo, conducta y contexto | Permitir un equipo conocido y reevaluar uno desconocido en otro país | Verify Explicitly |
| 5 | Se monitorea la integridad y postura de los activos | Revisar continuamente parcheo y configuración | Assume Breach |
| 6 | Autenticación y autorización se aplican dinámicamente antes del acceso | Confirmar identidad y permisos al solicitar nuevos recursos | Verify Explicitly |
| 7 | Se recopila información de activos, red y comunicaciones para mejorar seguridad | Analizar registros y comportamiento para ajustar políticas | Assume Breach |

La correspondencia con los tres principios es una **guía pedagógica del docente**, no una cita literal de NIST. Verificar explícitamente agrupa 1, 2, 4 y 6; mínimo privilegio agrupa 3; asumir la brecha agrupa 5 y 7.

---

## 4. Pilares y Dominios

CISA v2.0 presenta cinco pilares: Identidades, Dispositivos, Redes, Aplicaciones y Cargas de Trabajo, y Datos. Las capacidades transversales son Visibilidad y Analítica, Automatización y Orquestación, y Gobernanza.

El curso utiliza **seis dominios de trabajo**: los cinco pilares más Visibilidad y Analítica. Automatización y Orquestación se considera transversal; Gobernanza se relaciona también con [[Govern y Gobierno de Ciberseguridad|Govern del NIST CSF]]. Cada dominio se analiza mediante Protect, Detect, Respond y Recover.

---

## 5. Pilar Identidades: Cinco Funciones

### 5.1 Autenticación

Verifica que una identidad sea quien afirma ser antes de permitir acceso.

**Controles:** MFA, mecanismos resistentes a phishing como FIDO2, llaves físicas o WebAuthn; SSO con riesgo adaptativo; validación reforzada para recuperar cuentas.

**Caso:** el restablecimiento de MFA del caso MGM muestra que una mesa de ayuda puede convertirse en un punto de evasión de autenticación.

**Actividad:** diseñar un proceso de recuperación de MFA para una cuenta privilegiada con un mínimo de tres pasos de validación.

### 5.2 Repositorios de identidad

Incluye dónde y cómo se administran usuarios, cuentas de servicio, dispositivos y credenciales.

**Controles:** directorios centralizados (Active Directory, Entra ID/Azure AD o LDAP), integración de repositorios fragmentados y gestión segura de secretos en código o configuraciones.

**Caso:** el material relaciona LastPass (2022) con credenciales y secretos expuestos en repositorios de código, que facilitaron un segundo ataque.

**Actividad:** identificar repositorios de una universidad (correo, aula virtual, biblioteca o Wi-Fi) y discutir riesgos de su fragmentación.

### 5.3 Evaluación de riesgo de identidad

Analiza continuamente señales de comportamiento y contexto, además del inicio de sesión.

**Controles:** UEBA, puntuación de riesgo por accesos inusuales y capacidades ITDR. Las señales incluyen ubicación atípica, dispositivo nuevo, hora inusual o cambios de MFA y privilegios.

**Caso:** la presentación plantea que un cambio de MFA de una cuenta privilegiada solicitado por teléfono debió tratarse como una señal de riesgo en MGM.

**Actividad:** proponer tres señales concretas que permitan detectar una suplantación.

### 5.4 Gestión de acceso

Define las operaciones permitidas, los permisos y su ciclo de vida tras verificar la identidad.

**Controles:** RBAC, alta/cambio/baja formal, PAM y acceso Just-In-Time.

**Caso:** Twitter (2020). Según el material, la ingeniería social contra empleados con acceso a una herramienta administrativa permitió comprometer 130 cuentas de alto perfil para una estafa de Bitcoin.

**Actividad:** diseñar permisos para Agente de soporte N1, Agente N2, Supervisor y Administrador sobre acciones de ver perfil, resetear contraseña, verificar o suspender cuentas y modificar correo. El ejercicio requiere aplicar mínimo privilegio, sin una matriz de respuestas preestablecida en las diapositivas.

### 5.5 Visibilidad y analítica de identidad

Hace observable la actividad para detectar anomalías y sustentar auditorías.

**Controles:** registros centralizados de login y cambios de acceso, paneles de salud de identidades y auditorías periódicas de permisos.

**Caso:** la clase utiliza LastPass para discutir la visibilidad del uso indebido de credenciales de un ingeniero DevOps antes de detectar la exfiltración.

**Actividad:** proponer tres indicadores para un panel de salud de identidades.

### Síntesis del pilar

| Función | Pregunta principal |
| :--- | :--- |
| Autenticación | ¿Quién solicita acceso y cómo se verifica? |
| Repositorios | ¿Dónde se administran identidades y secretos? |
| Riesgo | ¿Qué señales cambian la confianza en la identidad? |
| Acceso | ¿Qué puede hacer y durante cuánto tiempo? |
| Visibilidad | ¿Podemos detectar y auditar su actividad? |

---

## 6. Pilar Dispositivos: Cinco Funciones

### 6.1 Cumplimiento de políticas

Aplica y monitorea las políticas de seguridad durante el uso del dispositivo.

**Controles:** MDM/UEM, líneas base de hardening y monitoreo continuo de cumplimiento.

**Caso:** según la presentación, un dispositivo personal usado por un ingeniero DevOps de LastPass tenía una versión vulnerable de Plex y carecía de monitoreo de cumplimiento.

**Actividad:** definir una lista de tres reglas mínimas que un dispositivo debe cumplir para acceder a sistemas corporativos.

### 6.2 Inventario y riesgo de proveedores

Mantiene el inventario de dispositivos y evalúa su origen y proveedores de hardware, firmware y software.

**Controles:** inventario actualizado (CIS Control 1), evaluación de proveedores y gestión de IoT y dispositivos externos.

**Caso:** Target y el proveedor Fazio Mechanical ilustran el riesgo de la cadena de suministro con acceso a la red.

**Actividad:** identificar tres tipos de dispositivos de terceros presentes en una universidad y evaluar su riesgo.

### 6.3 Acceso según postura

La decisión considera la salud del dispositivo junto con la identidad de quien lo utiliza.

**Controles:** acceso por cumplimiento, restricción de equipos desconocidos o no gestionados y verificación continua de postura.

**Caso positivo:** el Access Proxy de Google BeyondCorp evalúa postura en tiempo real para autorizar acceso a aplicaciones internas.

**Actividad:** diseñar una regla de acceso condicional para tres niveles distintos de postura.

### 6.4 Protección contra amenazas

Despliega y mantiene protección en endpoints.

**Controles:** EDR/XDR, antivirus administrado centralmente y aislamiento automático de equipos comprometidos.

**Caso:** el material describe un keylogger en el equipo personal del ingeniero de LastPass que capturó su contraseña maestra. Se usa para discutir la protección y detección en el endpoint.

**Actividad:** proponer un playbook de tres pasos ante detección de un keylogger.

### 6.5 Visibilidad y analítica de dispositivos

Permite observar estado y comportamiento para detectar anomalías y auditar la gestión.

**Controles:** telemetría centralizada, alertas de incumplimiento e inventario actualizado en tiempo real.

**Caso:** Equifax ilustra la falta de visibilidad sobre qué sistemas usaban la versión vulnerable de Apache Struts.

**Actividad:** proponer tres indicadores de dispositivos para anticipar incidentes.

### Síntesis del pilar

| Función | Pregunta principal |
| :--- | :--- |
| Cumplimiento | ¿Sigue las políticas y configuración segura? |
| Inventario y proveedores | ¿Sabemos qué equipo existe, de quién es y su origen? |
| Acceso por postura | ¿Su estado permite acceder al recurso? |
| Protección | ¿Podemos detectar y contener amenazas? |
| Visibilidad | ¿Tenemos datos actuales para revisar su salud? |

El video de Mirai (2016) introduce el riesgo de dispositivos IoT que pueden convertirse en parte de una botnet. Las diapositivas no desarrollan un procedimiento técnico de Mirai.

---

## 7. Protect, Detect, Respond y Recover

La tabla de cierre aplica las cuatro funciones a ambos dominios:

| Dominio | Protect | Detect | Respond | Recover |
| :--- | :--- | :--- | :--- | :--- |
| Identidades | MFA, mínimo privilegio y acceso condicional | Autenticaciones anómalas y cambios de privilegio | Revocar sesiones y bloquear identidad | Restaurar accesos y gestionar credenciales de emergencia |
| Dispositivos | Hardening, parches y control de aplicaciones | Comportamiento anómalo y vulnerabilidades | Aislar y contener el equipo | Reimagen y reincorporación segura |

La tabla organiza capacidades y procesos. Las tecnologías deben acompañarse de responsables, reglas de decisión y procedimientos de recuperación.

## 8. Conclusiones Clave

1. La recuperación de cuentas puede comprometer la autenticación si no incluye validación sólida.
2. Identidades y dispositivos aportan señales complementarias a una decisión de acceso.
3. Inventario, postura y telemetría deben actualizarse continuamente.
4. Proteger requiere también detectar, contener y recuperar con procesos definidos.

## 9. Referencias del Material

* Rose, S., Borchert, O., Mitchell, S. y Connelly, S. (2020). *Zero Trust Architecture*, [NIST SP 800-207](https://doi.org/10.6028/NIST.SP.800-207).
* Microsoft (2024). [Zero Trust Security and Strategy](https://www.microsoft.com/en-us/security/business/zero-trust).
* CISA (2023). [Zero Trust Maturity Model v2.0](https://www.cisa.gov/sites/default/files/2023-04/zero_trust_maturity_model_v2_508.pdf).
* Center for Internet Security (2024). [CIS Controls v8.1](https://www.cisecurity.org/controls/v8-1).
* Videos de clase: MGM Resorts, [LastPass](https://www.youtube.com/watch?v=8CA34e4ym-A) y [Mirai](https://www.youtube.com/watch?v=QXYlCW1WWVc). La presentación repite el mismo enlace para MGM y LastPass; se conserva como enlace de LastPass sin asignar un enlace independiente a MGM.
