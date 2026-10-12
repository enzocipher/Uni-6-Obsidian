---
tags:
  - ciberseguridad
  - procesos
  - zero_trust
  - nist_800_207
  - cisa
materia: Procesos de Ciberseguridad
unidad: 2
sesion: 5
ciclo: 6to
diapositivas: 20
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546139_1/file/_75895078_1?courseId=_546139_1
---

# Sesión 5: Zero Trust, Concepto y Principios

## 1. Objetivo de la Sesión

* Entender las limitaciones del modelo perimetral.
* Explicar la verificación explícita, el mínimo privilegio y la suposición de brecha.
* Relacionar controles con los pilares de Zero Trust.
* Reconocer la estructura de pilares y capacidades transversales de CISA.

---

## 2. Origen y Modelo Perimetral

### Caso de clase: Operation Aurora

La presentación utiliza Operation Aurora (2009) como antecedente de la evolución de Google hacia BeyondCorp y Zero Trust. La discusión se centra en por qué la ubicación dentro de una red no basta para confiar en un sujeto.

### Modelo de castillo y foso

En el modelo perimetral simplificado, el firewall protege el borde y se confía por defecto en lo que está dentro. Las limitaciones aparecen con trabajo remoto, BYOD, servicios cloud y atacantes que ya obtuvieron acceso interno.

Ejemplos del material: un empleado con credenciales comprometidas, un dispositivo personal infectado o un proveedor legítimo mal supervisado. En estos escenarios, la presencia en la red corporativa no demuestra que la conexión sea segura.

---

## 3. Concepto de Zero Trust

Zero Trust elimina la confianza implícita basada en ubicación, propiedad del dispositivo o afiliación y utiliza identidad, postura y contexto para evaluar el acceso a recursos. Es una estrategia organizacional que se implementa mediante procesos, políticas y capacidades técnicas.

NIST SP 800-207 (2020) formaliza la arquitectura Zero Trust. La sesión introduce una síntesis práctica de tres principios. La [[Identidades y Dispositivos en Zero Trust|Sesión 6]] distingue esta síntesis de Microsoft de los siete principios formales de NIST.

### Tres principios prácticos

| Principio | Qué exige | Ejemplo de clase |
| :--- | :--- | :--- |
| Verify Explicitly | Verificar explícitamente cada acceso con señales relevantes | Reevaluar un acceso desde un país distinto al habitual |
| Least Privilege | Limitar permisos y duración a lo necesario para la tarea | Acceso administrativo durante dos horas de mantenimiento |
| Assume Breach | Diseñar controles considerando que un atacante podría estar dentro | Impedir que una laptop de marketing comprometida alcance nóminas |

---

## 4. Controles por Principio

### 4.1 Verificación explícita

* MFA y evaluación de identidad en los accesos.
* Acceso condicional según ubicación, dispositivo, hora y comportamiento.
* Reevaluación continua de la sesión y sus señales de riesgo.
* SSO combinado con políticas de riesgo adaptativas.

La verificación continua puede provocar una nueva comprobación cuando el contexto cambia. La presentación la ilustra con un empleado que intenta acceder desde otro país una hora después de su acceso inicial.

### 4.2 Mínimo privilegio

* RBAC: permisos mínimos por rol.
* PAM: supervisión y registro de cuentas privilegiadas.
* Acceso Just-In-Time: elevación temporal y posterior revocación.
* Revisión y recertificación periódica de permisos.

Un permiso legítimo debe mantenerse solo mientras la tarea o responsabilidad lo justifique.

### 4.3 Asumir la brecha

* Microsegmentación para limitar movimiento lateral.
* EDR e ITDR para detectar actividad anómala de dispositivos e identidades.
* Cifrado de comunicaciones, también en la red interna.
* Planes de contención y aislamiento ante señales sospechosas.

---

## 5. Modelo de Madurez Zero Trust de CISA

### Pilares y capacidades transversales

| Pilares principales | Capacidades transversales |
| :--- | :--- |
| Identidades | Visibilidad y Analítica |
| Dispositivos | Automatización y Orquestación |
| Redes | Gobernanza |
| Aplicaciones y Cargas de Trabajo | |
| Datos | |

La agenda inicial menciona siete dominios, pero el desarrollo de esta sesión enumera **cinco pilares y tres capacidades transversales** del modelo CISA v2.0. En la sesión 6, el curso define seis dominios de trabajo al añadir Visibilidad y Analítica a los cinco pilares. Se mantienen estas distinciones para evitar confundir estructuras.

### Controles por pilar y principio

| Pilar | Verificar explícitamente | Mínimo privilegio | Asumir la brecha |
| :--- | :--- | :--- | :--- |
| Identidades | MFA, contexto y sesión | RBAC, PAM y JIT | UEBA y revocación de sesiones sospechosas |
| Dispositivos | Postura, parches, antivirus y certificados | Acceso por cumplimiento y restricciones de instalación | EDR y aislamiento automático |
| Redes | ZTNA y autenticación de conexiones | Microsegmentación por recurso | Monitoreo este-oeste y contención de segmentos |
| Aplicaciones y cargas | Autenticación servicio a servicio | Roles IAM por microservicio y gestión segura de secretos | Escaneo de vulnerabilidades, sandboxing y aislamiento |
| Datos | Identidad y contexto antes del acceso | Clasificación, necesidad de saber y cifrado | DLP y detección de exfiltración |

---

## 6. Actividades y Continuidad del Curso

La clase propone identificar tres situaciones cotidianas en las que estar dentro de la red no garantice confianza y explicar el riesgo en cada una.

La unidad 2 continúa con Identidades y Dispositivos en la sesión 6 y Aplicaciones y Datos en la sesión 7. La sesión 8 corresponde al examen parcial, según el cronograma mostrado.

## 7. Conclusiones Clave

1. La confianza por ubicación resulta insuficiente en entornos distribuidos.
2. Zero Trust combina identidad, postura y contexto para decidir accesos.
3. Mínimo privilegio y contención reducen el alcance de una credencial o equipo comprometido.
4. Los pilares requieren también visibilidad, automatización y gobernanza.

## 8. Referencias del Material

* Rose, S., Borchert, O., Mitchell, S. y Connelly, S. (2020). *Zero Trust Architecture*, NIST SP 800-207.
* Pascoe, C., Quinn, S. y Scarfone, K. (2024). *The NIST Cybersecurity Framework (CSF) 2.0*, NIST CSWP 29.
* CISA (2023). *Zero Trust Maturity Model*, versión 2.0.
* Video de clase: [Operation Aurora](https://www.youtube.com/watch?v=eZSY9MnKMP0).
