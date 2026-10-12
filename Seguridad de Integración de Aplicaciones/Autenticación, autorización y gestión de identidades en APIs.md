---
tags: [integracion, apis, iam, oauth, oidc, jwt]
materia: Seguridad de Integración de Aplicaciones
unidad: 2
sesion: 5
ciclo: 6to
diapositivas: 48
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546137_1/file/_75928332_1?courseId=_546137_1
---

# Sesión 5: Autenticación, autorización y gestión de identidades en APIs

## 1. Objetivo

Definir quién puede acceder a cada API, qué acciones puede realizar y qué límites deben aplicarse. El trabajo parte del TO-BE y convierte las interacciones en decisiones de acceso.

Una API expone una capacidad de negocio: consultar clientes, crear pedidos, modificar información o procesar pagos. El impacto de utilizarla indebidamente depende de esa capacidad y de su contexto.

## 2. Conocer las APIs antes de protegerlas

| Contexto | Descripción |
|---|---|
| Interna | Utilizada dentro de la organización |
| Pública | Disponible para consumidores externos |
| Partner | Disponible para socios específicos |
| Externa | Capacidad de un tercero que la organización consume |

El consumidor puede ser un usuario, una aplicación, un servicio, un socio o un sistema externo. Debe distinguirse la aplicación que hace la llamada de la identidad humana en cuyo nombre actúa.

En el ejemplo docente de TiendaModa.pe y Culqi, el cliente inicia la compra, la aplicación solicita el pago, un servicio interno puede conciliar o notificar resultados, un partner puede intercambiar información autorizada y un ERP externo puede registrar ingresos o preparar reportes. Cada participante tiene una función y necesidad de acceso distinta.

La criticidad se determina preguntando qué capacidad expone, qué proceso soporta, qué impacto tendría su uso indebido y qué riesgo se identificó previamente.

| Nivel ilustrativo | Criterio | Ejemplo |
|---|---|---|
| Baja | Capacidad informativa o de apoyo; afectación limitada | Catálogo de productos |
| Media | Proceso importante con afectación parcial o recuperable | Promociones o disponibilidad |
| Alta | Información sensible o proceso relevante | Clientes |
| Crítica | Proceso esencial o transacciones de alto valor | Pagos |

## 3. Catálogo de APIs v1

| Campo | Contenido |
|---|---|
| API | Nombre identificable |
| Propósito | Capacidad que expone |
| Proveedor o responsable | Sistema, servicio o dominio responsable |
| Consumidores | Participantes que necesitan utilizarla |
| Exposición | Contexto de acceso |
| Criticidad | Consecuencia de uso indebido o falla |
| Riesgo asociado | Escenario relacionado, cuando corresponda |

El proveedor puede ser un sistema de pedidos, un servicio especializado de pagos o un dominio como servicio al cliente. El catálogo responde **qué se debe proteger**.

Los niveles de criticidad de los ejemplos son contextuales: la presentación muestra una API de pagos crítica en una explicación y media en otro catálogo ilustrativo. Para el proyecto se debe justificar un nivel consistente con el proceso analizado.

## 4. AuthN, AuthZ e IAM

| Concepto | Pregunta | Resultado |
|---|---|---|
| Autenticación, AuthN | ¿Quién eres? | Identidad verificada |
| Autorización, AuthZ | ¿Qué puedes hacer? | Acciones y recursos permitidos |
| IAM | ¿Cómo gestionamos identidades y accesos? | Roles, permisos, políticas y ciclo de vida coherentes |

Una identidad verificada puede estar autorizada para consultar y crear, pero no para aprobar o eliminar. La autenticación no concede acceso ilimitado.

IAM abarca usuarios, aplicaciones y servicios. El acceso debe gestionarse de manera consistente durante su ciclo de vida.

El ejemplo de pagos desarrolla cinco elementos: identidades de comercio, app, operadores y servicios; roles de comercio, soporte, analista y administrador; permisos para crear cargos o consultar pagos; políticas de acceso; y ciclo de vida con alta, cambio, revocación y rotación de credenciales. También señala la **trazabilidad**: cada operación debe quedar registrada.

## 5. Mínimo privilegio

Otorgar acceso únicamente a los recursos y acciones que la necesidad de negocio exige. La pregunta es **cuál es el mínimo acceso necesario**.

Para una consulta de pedidos propios puede requerirse `pedidos:read`; no se justifican por esa necesidad modificar pedidos, administrarlos o consultar los de otros clientes. La restricción del recurso concreto debe figurar en el modelo.

En el ejemplo de integración de pagos, la app del comercio necesita crear pagos y consultar su estado, con acceso al ámbito del propio comercio. La presentación excluye modificar datos de otros clientes, eliminar transacciones, administrar credenciales globales o cambiar configuraciones internas del proveedor.

## 6. Selección de mecanismos

Antes de elegir tecnología:

1. Identificar consumidor y contexto.
2. Definir si la identidad es humana, aplicación o servicio.
3. Determinar acciones y recursos permitidos.
4. Evaluar criticidad y riesgos.
5. Elegir el mecanismo y justificarlo.

Entre los mecanismos mencionados aparecen API Key, mTLS y OIDC; OAuth 2.0 se relaciona con autorización y delegación. JWT es un formato posible de token.

### Modelos y reglas de autorización

| Modelo o mecanismo | Cómo decide el acceso | Ejemplo docente |
|---|---|---|
| RBAC | Según el rol de persona o aplicación | Soporte puede consultar pagos, sin eliminarlos |
| ABAC | Según atributos de usuario, recurso, acción o contexto | Acceso si área es Finanzas y sede es Lima |
| ACL | Lista de permisos por recurso | Ana puede leer un archivo; Pedro puede leerlo y modificarlo |
| Scopes | Delimitan operaciones del token o aplicación | `payments.read`, `payments.create` |
| Políticas | Combinan condiciones para permitir o bloquear | Modificación solo desde la red corporativa |
| OAuth 2.0 | Autorización delegada con acceso limitado | Consultar pagos sin administrar credenciales |
| Claims | Utilizan declaraciones del token, como rol o atributos | Rol auditor permite consultas |

### Mecanismos de autenticación

| Mecanismo | Idea |
|---|---|
| Usuario y contraseña | Identificador y secreto para demostrar identidad |
| MFA / 2FA | Combina más de un factor: conocimiento, posesión o característica personal |
| Biometría | Verificación mediante una característica física o biométrica |
| Certificado digital | Identidad vinculada a material criptográfico |
| mTLS | Cliente y servidor se autentican mutuamente mediante certificados |
| Kerberos | Autenticación basada en tickets |
| SAML 2.0 | Federación de identidad, utilizada en SSO empresarial |
| OIDC | Capa de identidad sobre OAuth 2.0 |

### OAuth 2.0

Permite que una aplicación obtenga acceso limitado a recursos sin recibir directamente las credenciales del usuario.

| Actor | Papel |
|---|---|
| Resource Owner | Dueño de los recursos |
| Client | Aplicación que solicita acceso |
| Authorization Server | Emite tokens de acceso y administra la autorización |
| Resource Server | Aloja el recurso y valida el acceso presentado |

OAuth se centra en la **autorización delegada**. El modelo debe describir qué recursos y acciones permite la delegación.

### OpenID Connect, OIDC

Capa de identidad sobre OAuth 2.0 que permite conocer al usuario autenticado. La sesión resume la relación como **OAuth + identidad**.

- OAuth: acceso autorizado a recursos.
- OIDC: autenticación e información de identidad.

Son problemas relacionados que cumplen funciones distintas en el modelo.

La ilustración distingue el **ID Token**, que utiliza la aplicación para conocer al usuario autenticado, del **Access Token**, que se presenta para acceder al recurso protegido. En el ejemplo, la app recibe identidad y acceso autorizado para consultar pagos; la API valida el access token y los permisos de la operación.

### Tokens y JWT

Un token comunica información asociada a identidad o acceso: sujeto, emisor, audiencia, permisos y expiración. El cliente lo presenta y la API valida lo que corresponda.

Un JWT firmado tiene la forma:

```text
header.payload.signature
```

| Parte | Contenido |
|---|---|
| Header | Metadatos como algoritmo y tipo |
| Payload | Claims o declaraciones |
| Signature | Verificación de integridad y autenticidad del token firmado |

Claims frecuentes: `sub` identifica al sujeto, `iss` al emisor, `aud` a la audiencia y `exp` a la expiración. No todo token es JWT, y usar JWT no vuelve segura automáticamente una API.

La API debe verificar que el token sea válido, no haya vencido, corresponda al destinatario y contenga el permiso requerido. Después aplica las restricciones del recurso solicitado.

| Tipo de token | Para qué sirve |
|---|---|
| Access Token | Acceder a APIs según permisos concedidos |
| ID Token | Comunicar la identidad del usuario autenticado |
| Refresh Token | Obtener un nuevo access token según el flujo y la política de renovación |
| Session Token | Mantener identificada una sesión activa |

| Formato o representación | Característica que señala el material |
|---|---|
| JWT | Estructura de header, payload y firma en el ejemplo |
| Token opaco | Cadena cuyo contenido no se interpreta directamente |
| PASETO | Formato alternativo con modos de firma o cifrado |
| SAML Assertion | Representación XML de identidad utilizada en SSO |

El tipo describe la finalidad; el formato describe cómo se representa. Son dos dimensiones diferentes.

## 7. Del catálogo al modelo de acceso

Todas las APIs deben tener una decisión de acceso. Si una API tiene distintos consumidores o reglas, puede necesitar varias filas.

El modelo tiene dos vistas complementarias:

- **Diagrama:** cómo sucede el acceso; consumidores, identidades, AuthN, APIs, AuthZ, permisos y restricciones.
- **Matriz:** quién puede hacer qué, con qué mecanismo, bajo qué límites y por qué.

| API | Consumidor / identidad | AuthN | AuthZ | Permiso | Restricción | Justificación |
|---|---|---|---|---|---|---|
| Pedidos | Web o app / usuario | OIDC | Consultar sus pedidos | `pedidos:read` | No consultar pedidos ajenos | Evitar exposición de otros clientes |
| Pagos | Web o app / usuario | OIDC | Procesar pagos autorizados | `pagos:create` | No administrar pagos ni realizar transacciones ajenas | Limitar la operación a la necesidad |
| Pólizas | Aplicación interna / servicio | Mecanismo definido para el servicio | Consultar pólizas autorizadas | `polizas:read` | No modificar ni consultar fuera de su ámbito | Proteger información sensible |

El ejemplo de pólizas deja pendiente precisar el mecanismo del servicio. Una implementación requiere completar esa decisión.

## 8. Proyecto integrador: avance 5

1. Revisar propósito, consumidores, exposición, criticidad y riesgos del catálogo.
2. Identificar consumidor y tipo de identidad.
3. Definir AuthN.
4. Definir AuthZ, permisos o scopes.
5. Especificar restricciones por mínimo privilegio.
6. Justificar cada regla.
7. Construir el diagrama y comprobar su coherencia con la matriz y el catálogo.

Entregables: **catálogo de APIs v1 + modelo AuthN/AuthZ**, compuesto por diagrama y matriz de reglas.

## 9. Repaso

1. ¿Por qué la identidad de una app y la de su usuario pueden ser distintas?
2. ¿Qué responde OAuth y qué agrega OIDC?
3. ¿Por qué token y JWT no son sinónimos?
4. ¿Qué diferencia existe entre permiso de consulta y autorización sobre un objeto?
5. ¿Qué debe tener cada fila del modelo de acceso?

## Conexiones

- [[Security by Design y arquitectura TO BE]]
- [[Protección de datos durante la integración]]
- [[Identidades y Dispositivos en Zero Trust]]
- [[Dinámicas de integración, acceso y protección de datos]]
- [[Índice de Seguridad de Integración de Aplicaciones]]

## Fuente

Presentación **Sesion05_Clase_SIA.pptx**, 48 diapositivas, revisada en el aula virtual. Las diferencias de criticidad entre ejemplos se señalan para evitar tratarlas como reglas universales.
