---
tags: [integracion, arquitectura, apis, patrones, as-is]
materia: Seguridad de Integración de Aplicaciones
unidad: 1
sesion: 2
ciclo: 6to
diapositivas: 36
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546137_1/file/_75693860_1?courseId=_546137_1
---

# Sesión 2: Arquitecturas y patrones de Integración de Aplicaciones

## 1. Objetivo

Reconocer cómo colaboran los sistemas y representar la arquitectura **AS-IS**, es decir, su estado actual. La arquitectura define participantes, comunicaciones, información intercambiada, capacidades expuestas y coordinación.

Las alternativas pueden coexistir. Una organización puede tener un monolito, integraciones punto a punto, servicios y APIs dentro de un mismo ecosistema.

## 2. Alternativas arquitectónicas

| Alternativa | Característica | Consideración |
|---|---|---|
| Punto a punto | Conexiones directas entre aplicaciones | Sencilla con pocos participantes; crece el número de dependencias al aumentar sistemas |
| Cliente-servidor | Un cliente solicita una capacidad a un servidor | Distingue al consumidor del proveedor de la capacidad |
| Monolito | Presentación, lógica de negocio y acceso a datos forman una unidad | La coordinación interna es más concentrada |
| SOA | Servicios reutilizables que ofrecen capacidades de negocio | Facilita compartir servicios entre consumidores |
| APIs | Contratos para consumir capacidades | Requiere especificar solicitudes, datos y respuestas |
| Microservicios | Servicios pequeños e independientes por capacidad de negocio | Mayor independencia y opciones de escalado, con más complejidad operativa |
| Eventos | Componentes reaccionan a hechos publicados | Permite desacoplar al emisor de varios consumidores |

Más componentes no implican automáticamente una arquitectura mejor. Deben evaluarse el mantenimiento, la operación y la necesidad real del proceso.

## 3. APIs como contratos

Una API define qué se puede solicitar, cómo hacerlo, qué información se debe enviar y qué respuesta se espera. La capacidad expuesta puede consultar clientes, crear pedidos o ejecutar pagos.

### REST

Organiza la interacción alrededor de recursos, emplea operaciones HTTP y representaciones de datos. La sesión destaca interacciones sin estado de sesión del cliente almacenado entre solicitudes.

| Ejemplo | Intención |
|---|---|
| `GET /clientes` | Consultar clientes |
| `GET /clientes/123` | Consultar un cliente |
| `POST /clientes` | Crear un cliente |
| `PUT /clientes/123` | Actualizar la representación del cliente |

Los ejemplos describen el contrato funcional; los controles de acceso se desarrollan en la sesión 5.

### SOAP

Utiliza mensajes XML y un contrato formal de operaciones. La estructura incluye un **Envelope**, un **Header** opcional y un **Body** con el contenido. El material lo relaciona con estándares de la familia WS-*.

REST y SOAP son formas de interacción que deben entenderse según el contexto del sistema y sus requisitos.

## 4. Microservicios y gateway

Los microservicios pueden separar capacidades como usuarios, pedidos, pagos e inventario. Su independencia permite evolucionar o escalar capacidades específicas; también introduce más comunicaciones y componentes que operar.

Un **API Gateway** puede actuar como punto de entrada para web, aplicaciones móviles y socios. Entre sus responsabilidades pueden aparecer enrutamiento, composición, transformación y administración del acceso a APIs. Debe quedar claro qué responsabilidades conserva cada servicio.

## 5. Comunicación síncrona y asíncrona

| Modalidad | Comportamiento | Efecto que debe analizarse |
|---|---|---|
| Síncrona | El emisor espera una respuesta para continuar | Latencia y dependencia inmediata de la disponibilidad del receptor |
| Asíncrona | El emisor envía información y puede continuar | Coordinación posterior y seguimiento del resultado |

Ejemplo orientado a eventos: **pedido creado** puede desencadenar procesamiento del pago, actualización del inventario y envío de una notificación.

## 6. Patrones de integración

| Patrón | Idea |
|---|---|
| Request-reply | Una solicitud recibe una respuesta |
| Publicación-suscripción | Un evento publicado llega a consumidores suscritos |
| Cola de mensajes | Los mensajes esperan a ser procesados por consumidores |
| Enrutamiento | El mensaje se dirige al destino que corresponde |

El diagrama debe representar el patrón que realmente existe. Si una característica técnica no se conoce, se declara como supuesto y se justifica.

## 7. Criterios para comparar alternativas

- **Acoplamiento:** cuánto depende una aplicación de las decisiones de otra.
- **Escalabilidad:** capacidad para soportar crecimiento de uso o carga.
- **Mantenibilidad:** facilidad para cambiar y operar la solución.
- **Reutilización:** capacidad de compartir servicios o capacidades.
- **Interoperabilidad:** intercambio útil de información.
- **Complejidad:** esfuerzo de construcción, coordinación y operación.

La decisión debe conectar necesidades y restricciones con una alternativa. Volumen, latencia, disponibilidad, costos, uso de terceros e innovación pueden modificar la comparación. Independencia y flexibilidad pueden exigir más esfuerzo operativo.

## 8. Proyecto integrador: avance 2

El resultado es un **AS-IS comprensible y justificado**:

1. Seguir el proceso: quién participa, qué intercambia y para qué.
2. Identificar integraciones existentes: directas, servicios, APIs, sincronía, asincronía o eventos, según corresponda.
3. Construir un diagrama con sistemas, aplicaciones, organizaciones y flujos.
4. Explicar dos o tres decisiones del AS-IS: necesidad, beneficio, contrapartida y razón.
5. Declarar y justificar los supuestos sobre detalles desconocidos.

### Caso de tienda online

El cliente se registra, selecciona productos, paga y recibe confirmación y despacho. Participan web o app, pedidos, inventario, un componente interno de pagos, un proveedor externo de pagos y logística.

La lectura del AS-IS permite discutir:

- Qué integra directamente la web y por qué.
- Qué responsabilidad cumple el componente interno de pagos.
- Cómo se coordinan pedidos e inventario.
- Qué información se intercambia con pagos y logística.
- Qué dependencias y límites organizacionales aparecen.
- Qué supuesto sostiene cada protocolo o mecanismo dibujado.

La automatización y la actualización de información son beneficios; el acoplamiento y la dependencia de terceros son aspectos que deben explicarse. Nombrar HTTPS no describe por sí solo todo el modelo de autenticación y autorización.

## 9. Repaso

1. ¿Cómo distinguir SOA, API y microservicios?
2. ¿Cuándo puede importar la dependencia de una llamada síncrona?
3. ¿Qué representa un evento y quién lo consume?
4. ¿Qué contrapartida tiene una arquitectura más distribuida?
5. ¿Cómo reconocer un supuesto en un AS-IS?

## Conexiones

- [[Fundamentos de Integración de Aplicaciones]]
- [[Riesgos y vulnerabilidades en integraciones]]
- [[Frameworks de arquitectura de seguridad]]
- [[Índice de Seguridad de Integración de Aplicaciones]]

## Fuente

Presentación **Sesion02_Arquitecturas de Integración.pptx**, 36 diapositivas, revisada en el aula virtual. Incluye la explicación textual del ejemplo visual del proyecto.
