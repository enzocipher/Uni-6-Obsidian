---
tags: [integracion, practica, casos, authn, authz, datos]
materia: Seguridad de Integración de Aplicaciones
tipo: practica
unidad: 2
ciclo: 6to
diapositivas: 29
fuentes:
  - https://aulavirtual.upc.edu.pe/ultra/courses/_546137_1/file/_75851641_1?courseId=_546137_1
  - https://aulavirtual.upc.edu.pe/ultra/courses/_546137_1/file/_75928330_1?courseId=_546137_1
  - https://aulavirtual.upc.edu.pe/ultra/courses/_546137_1/file/_76003693_1?courseId=_546137_1
---

# Dinámicas de integración, acceso y protección de datos

Tres presentaciones de práctica de las semanas 4, 5 y 6. Se conservan las consignas académicas y las respuestas que aparecen en el material. Las consignas abiertas siguen siendo ejercicios para resolver.

## 1. Simulacro de diseño seguro: MediTurno

**Fuente:** Dinamica-Simulacro.pptx, 6 diapositivas.

MediTurno es una clínica que permite reservar citas desde una aplicación web:

```text
Web de Citas → Sistema de Citas
Sistema de Citas → Sistema de Pacientes
Sistema de Citas → Proveedor externo de Agenda Médica
Sistema de Citas → Servicio de Notificaciones
```

La web envía la solicitud; el sistema consulta datos del paciente y horarios del proveedor externo. Al confirmar la reserva, envía la confirmación a notificaciones.

### Ronda 1: entender

Elegir una integración relevante e identificar productor, consumidor, información y propósito. Pueden elegirse intercambios distintos, siempre que sean coherentes con el caso.

### Ronda 2: analizar

| Condición | Hecho que debe analizarse |
|---|---|
| A | Citas puede consultar toda la información del paciente, aunque necesita solo datos básicos |
| B | La web se comunica directamente con Citas, expuesto para recibir solicitudes desde Internet |
| C | La consulta de horarios depende del proveedor externo; si no responde, el sistema espera y el paciente no puede continuar |

Elegir una condición y construir **activo → amenaza → vulnerabilidad → riesgo → impacto**. Una condición por sí sola no es un escenario completo. En esta ronda se analiza antes de proponer una solución.

### Ronda 3: decidir

Partir del riesgo elegido:

1. Identificar la propiedad CIA principalmente afectada.
2. Seleccionar un principio principal de Security by Design.
3. Proponer una decisión arquitectónica.
4. Justificar cómo aplica el principio y reduce el riesgo.

El criterio de evaluación es la relación defendible entre los elementos de la cadena. Mencionar más principios no sustituye la justificación.

### Ronda 4: rediseñar

Construir el TO-BE preservando el proceso de reserva. Explicar qué cambia y cómo reduce el riesgo. Se pueden agregar, eliminar o modificar componentes o relaciones si la decisión lo justifica.

**Cadena completa:** AS-IS → riesgo → CIA → principio → decisión → TO-BE.

El simulacro deja la solución abierta para la discusión de los grupos.

## 2. Modelo de acceso: Mi Web de Seguros

**Fuente:** Dinamica.pptx, 10 diapositivas. Las diapositivas son imágenes; las tablas y respuestas siguientes se transcriben de su contenido visual.

El cliente desea consultar su póliza **P001**. El recorrido es cliente, Mi Web de Seguros, API Consulta Datos Póliza y base de datos Azure.

### Ronda 1: reconocer la capacidad

| Pregunta | Respuesta del material |
|---|---|
| ¿Qué capacidad expone la API? | Consultar información de una póliza |
| ¿Quién la consume? | Mi Web de Seguros en nombre del cliente |
| ¿Cualquiera puede utilizarla? | Solo clientes autenticados y autorizados, porque hay datos sensibles |
| ¿Qué debe decidirse antes del acceso? | Quién accede y qué está autorizado a hacer |

### Ronda 2: catalogar

La web es accesible desde Internet. La API es interna y transversal; no está expuesta directamente a Internet. Que la web sea pública no convierte automáticamente a todas sus APIs internas en públicas.

| Campo | Solución del caso |
|---|---|
| Nombre | API Consulta Datos Póliza |
| Propósito | Consultar información de pólizas |
| Responsable | Dominio Servicio al Cliente |
| Consumidor | Mi Web de Seguros |
| Exposición | Interna |
| Criticidad | Alta |
| Riesgo | Acceso no autorizado a información sensible de pólizas |

### Ronda 3: AuthN, AuthZ y mínimo privilegio

El cliente ya inició sesión y P001 le pertenece. La funcionalidad es únicamente de consulta.

- **AuthN:** verificar la identidad del cliente que inició sesión.
- **AuthZ:** autorizar la consulta de P001 porque pertenece a ese cliente.
- **Mínimo privilegio:** consultar sus propias pólizas; sin crear, modificar, eliminar o acceder a las de otros clientes.

Primero se define la necesidad de acceso y después se eligen los mecanismos.

### Ronda 4: mecanismos

José Lam consulta su propia póliza P001. La web llama a la API en su nombre y utiliza un access token con formato JWT.

| Elemento | Respuesta del material |
|---|---|
| Identidad | OIDC autentica al usuario y establece su identidad |
| Delegación | OAuth 2.0 permite a la web acceder en nombre del usuario mediante un access token |
| Token | JWT es el formato utilizado en este escenario |
| Validación | Comprobar firma, emisor `iss`, audiencia `aud`, expiración `exp` y permiso `polizas:read` |
| Recurso | Comprobar que P001 pertenece al usuario autorizado |

**Un token válido con `polizas:read` no concede acceso a cualquier póliza.** Si el mismo usuario solicita P002 y pertenece a otro cliente, la API debe denegar esa consulta.

### Ronda 5: modelo completo

El diagrama y la matriz reúnen las decisiones anteriores:

```text
IAM → José Lam / usuario → OIDC / AuthN
    → API Consulta Datos Póliza → OAuth 2.0 / AuthZ
    → polizas:read → consultar P001
    → verificar pertenencia y restringir otras acciones
```

| API | Consumidor | Identidad | AuthN | AuthZ | Permiso | Restricciones | Justificación |
|---|---|---|---|---|---|---|---|
| Consulta Datos Póliza | Mi Web de Seguros en nombre de José | Usuario | OIDC | Consultar pólizas autorizadas | `polizas:read` | No crear, modificar o eliminar; no consultar pólizas ajenas | Aplicar mínimo privilegio y proteger datos sensibles |

El flujo conceptual resume funciones del modelo; no pretende describir un intercambio completo del protocolo OAuth u OIDC.

## 3. Protección de datos: Banco Nova

**Fuente:** Dinamica v2.pptx, 13 diapositivas. Se transcribe el contenido visual de las seis rondas y sus soluciones.

Banco Nova permite solicitar una tarjeta virtual desde su app móvil. La **API Emisión Tarjeta Virtual** es externa, crítica y soporta la generación del producto. El recorrido continúa hacia la Plataforma de Tarjetas.

### Ronda 1: del acceso a los datos

Camila Torres está autenticada y autorizada para solicitar el producto. Esto responde quién accede y qué puede hacer. Aún debe analizarse **qué información circula y cómo protegerla**.

### Ronda 2: tipo, sensibilidad e impacto

Camila solicita una tarjeta virtual con límite de S/ 3,000. Los valores son ejemplos ficticios del material.

| Dato | Valor de ejemplo | Tipo | Sensibilidad | Razón |
|---|---|---|---|---|
| Identificador de cliente | CLI-58421 | Personal | Confidencial | Identifica al cliente dentro del servicio |
| Tipo de producto | Tarjeta Virtual | Negocio | Interna | Aislado revela información limitada del producto solicitado |
| Cuenta asociada | 001-45879 | Transaccional | Confidencial | Expone información bancaria vinculada al cliente |
| Límite solicitado | S/ 3,000 | Transaccional | Confidencial | Revela una condición económica de la solicitud |
| Moneda | PEN | Transaccional | Interna | Aislada presenta menor impacto |
| Dispositivo de origen | DEV-7854 | Técnica | Interna | Identifica información técnica utilizada por el servicio |
| Token de acceso | Oculto en la presentación | Credencial o token | Restringida o crítica | Su exposición puede facilitar uso indebido del acceso |

El tipo del dato no determina por sí solo su sensibilidad. La tabla es una clasificación contextual del caso.

### Ronda 3: riesgos durante la transmisión

| Situación | Riesgo | Impacto | Necesidad |
|---|---|---|---|
| Un tercero observa cuenta y límite | Intercepción | Exposición de información confidencial | Confidencialidad |
| Un tercero cambia S/ 3,000 por S/ 10,000 | Modificación | Procesar una solicitud alterada | Integridad |
| La app se conecta con un servicio que suplanta a la API | Suplantación | Entregar datos a un servicio no legítimo | Autenticidad |

### Ronda 4: proteger el canal app → API

| Necesidad | Control y ubicación | Qué aporta |
|---|---|---|
| Confidencialidad | HTTPS sobre TLS entre app y API | Cifra la comunicación en tránsito |
| Integridad | Protección de integridad de TLS en ese canal | Permite detectar alteraciones del tráfico protegido |
| Autenticidad | TLS con validación del certificado de la API mediante una PKI de confianza | Verifica la identidad del servicio antes de confiar en él |

Una decisión completa identifica mecanismo, ubicación y propiedad protegida.

### Ronda 5: proteger la solicitud como contenido

La API envía una Solicitud de Emisión a la Plataforma de Tarjetas. El caso exige que los componentes no autorizados no puedan leerla y que la plataforma pueda detectar alteración y verificar su origen.

| Requisito | Necesidad | Solución del material |
|---|---|---|
| Contenido ilegible para componentes no autorizados | Confidencialidad | Cifrar la Solicitud de Emisión antes de enviarla a la plataforma |
| Detectar alteración y verificar origen | Integridad y autenticidad | Firmar digitalmente la solicitud antes de enviarla |

La firma conserva el objetivo de verificar contenido y origen; el cifrado protege la confidencialidad. Estos mecanismos pueden complementarse con TLS.

### Ronda 6: justificar la decisión completa

| Datos | Sensibilidad | Riesgo | Necesidad | Control y ubicación | Justificación |
|---|---|---|---|---|---|
| Cuenta y límite | Confidencial | Intercepción | Confidencialidad | HTTPS/TLS en app → API | Evitar lectura del tráfico interceptado |
| Límite | Confidencial | Modificación | Integridad | Integridad de TLS en app → API | Detectar alteraciones del tráfico |
| Datos de solicitud | Confidencial | Suplantación | Autenticidad | Validar certificado de la API mediante PKI de confianza | Verificar al servicio receptor |
| Solicitud de Emisión | Confidencial | Exposición a componentes no autorizados | Confidencialidad | Cifrado antes de enviar a Plataforma de Tarjetas | Mantener el contenido ilegible para esos componentes |
| Solicitud de Emisión | Confidencial | Alteración u origen no verificable | Integridad y autenticidad | Firma digital antes del envío | Detectar cambios y verificar origen |

**Trazabilidad:** datos → sensibilidad → riesgo → necesidad → control → justificación.

## 4. Preguntas para practicar sin mirar las soluciones

1. Construir un riesgo de MediTurno y defender su cambio en el TO-BE.
2. Explicar por qué una API interna de pólizas necesita controles de acceso.
3. Explicar por qué un token válido no autoriza la lectura de P002.
4. Clasificar los datos de Banco Nova y justificar cada sensibilidad.
5. Ubicar la protección del canal y la del contenido en los dos flujos de Banco Nova.
6. Explicar qué se pierde si se firma un mensaje, pero se deja legible para participantes no autorizados.

## Conexiones

- [[Riesgos y vulnerabilidades en integraciones]]
- [[Security by Design y arquitectura TO BE]]
- [[Autenticación, autorización y gestión de identidades en APIs]]
- [[Protección de datos durante la integración]]
- [[Índice de Seguridad de Integración de Aplicaciones]]
