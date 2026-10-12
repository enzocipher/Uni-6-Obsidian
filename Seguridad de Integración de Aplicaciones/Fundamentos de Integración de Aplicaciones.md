---
tags: [integracion, aplicaciones, procesos, interoperabilidad]
materia: Seguridad de Integración de Aplicaciones
unidad: 1
sesion: 1
ciclo: 6to
diapositivas: 30
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546137_1/file/_75504108_1?courseId=_546137_1
---

# Sesión 1: Fundamentos de Integración de Aplicaciones

## 1. Objetivo

Comprender el negocio, sus procesos y su ecosistema antes de decidir cómo integrar aplicaciones. Una integración conecta sistemas, información, personas y actividades para producir un resultado de negocio.

La pregunta inicial es **qué necesita colaborar y para qué**. Elegir una API, un protocolo o una plataforma viene después de entender esa necesidad.

## 2. Por qué integrar

Las organizaciones utilizan aplicaciones especializadas. Un proceso suele atravesar varias de ellas y puede depender también de servicios externos.

| Proceso | Aplicaciones o participantes que colaboran | Resultado esperado |
|---|---|---|
| Compra y pago | Tienda, proveedor de pagos y banco | Confirmar una compra y su pago |
| Gestión de pedidos | Plataforma de pedidos, proveedor y reparto | Entregar el producto |
| Acceso a información | Identidad, aplicación y repositorio de datos | Permitir la consulta correspondiente |
| Reserva | Disponibilidad, reservas y pagos | Confirmar una reserva válida |

La integración permite que un cambio o solicitud en un sistema sea utilizado por otro. Tiene sentido cuando soporta una necesidad del negocio y mantiene la información coherente.

## 3. Proceso de negocio y recorrido del usuario

Un **proceso de negocio** es un conjunto de actividades relacionadas que producen un resultado. El recorrido que observa el usuario puede parecer sencillo, aunque por detrás intervengan varios sistemas.

Ejemplo de compra:

1. El cliente busca y selecciona un producto.
2. Se valida el stock.
3. Se procesa el pago.
4. Se registra el pedido.
5. Se actualiza el inventario.
6. Se envía la confirmación.

La aplicación web o móvil ofrece la experiencia visible. Catálogo, inventario, pagos, pedidos y notificaciones colaboran para completar el proceso. Para estudiar una integración se debe vincular cada intercambio con la actividad que permite realizar.

## 4. Ecosistema de aplicaciones

| Ámbito | Ejemplos | Pregunta de análisis |
|---|---|---|
| Interno | Web, ERP, CRM, sistemas core y bases de datos | ¿Qué capacidad ofrece cada sistema y quién es responsable? |
| Externo | Bancos, proveedores, pagos, servicios cloud, instituciones y socios | ¿Qué necesidad cubre el tercero y de qué depende el proceso? |

El límite de la organización ayuda a identificar responsabilidades. Tener un proveedor externo introduce una dependencia que debe figurar en el mapa del ecosistema.

Un inventario inicial debe permitir reconocer la aplicación, su propósito, la información que maneja y los procesos en los que participa. El mapa muestra cómo esas aplicaciones se relacionan.

## 5. Productor, consumidor e información

| Elemento | Significado |
|---|---|
| Productor | Origina o proporciona la información |
| Consumidor | Necesita y utiliza la información |
| Información intercambiada | Datos que permiten continuar una actividad |
| Propósito | Necesidad de negocio que justifica el intercambio |

Entre los datos habituales aparecen clientes, pedidos, productos, pagos, matrículas, historias clínicas y pólizas. La identificación debe realizarse **por intercambio**: una aplicación puede producir datos en una interacción y consumirlos en otra.

Ejemplo: el sistema de pedidos comunica un pedido al sistema de inventario para reservar productos. Nombrar las dos aplicaciones no basta; también se debe explicar qué datos circulan y qué actividad soportan.

## 6. Interoperabilidad

La interoperabilidad consiste en **intercambiar información y poder utilizarla con un significado compatible**. Una conexión técnica por sí sola no demuestra que los sistemas comprendan los datos de la misma manera.

| Diferencia entre sistemas | Necesidad de integración |
|---|---|
| `CustomerID` frente a `IDCliente` | Correspondencia entre campos |
| Nombre completo frente a nombres y apellidos separados | Transformación de la estructura |
| Formatos diferentes de fecha | Conversión y validación |
| Conceptos o reglas de negocio diferentes | Alinear el significado y las reglas |

La integración puede requerir traducir formatos, transformar estructuras, validar valores y aplicar reglas del negocio. Si el significado se pierde, un mensaje técnicamente recibido puede producir una decisión equivocada.

## 7. Dimensiones que deben observarse

| Dimensión | Pregunta |
|---|---|
| Negocio | ¿Por qué se necesita integrar? |
| Procesos | ¿Qué actividades deben colaborar? |
| Personas | ¿Quién participa? |
| Datos | ¿Qué información se intercambia? |
| Sistemas | ¿Qué aplicaciones intervienen? |
| Organización | ¿Quién asume la responsabilidad? |

El curso presenta una evolución desde aplicaciones aisladas y cliente-servidor hasta SOA, APIs, microservicios, cloud y ecosistemas digitales. Estas opciones responden a contextos y necesidades distintos.

## 8. Efecto de una falla

Una falla en un componente puede interrumpir una integración, detener una actividad y afectar todo el proceso. El resultado puede incluir demoras, errores operativos, perjuicio al cliente, pérdidas económicas y daño reputacional.

Las decisiones de ingeniería tienen consecuencias financieras, organizacionales, sociales y de seguridad. Por eso el análisis debe seguir el proceso completo y sus dependencias.

## 9. Proyecto integrador: avance 1

El primer avance construye la comprensión del escenario:

- Describir el negocio y el proceso seleccionado.
- Identificar participantes, actividades y aplicaciones.
- Reconocer los datos y los intercambios necesarios.
- Preparar el inventario de aplicaciones y el mapa preliminar del ecosistema.
- Explicar el propósito de las integraciones.

Este avance proporciona la entrada para representar la arquitectura actual en la siguiente sesión.

## 10. Repaso

1. ¿Qué resultado produce el proceso y qué sistemas necesita?
2. ¿Quién produce y quién consume la información en cada intercambio?
3. ¿Qué diferencia existe entre conexión e interoperabilidad?
4. ¿Cómo afecta al negocio la falla de una integración externa?
5. ¿Qué información falta antes de elegir una arquitectura?

## Conexiones

- [[Arquitecturas y patrones de Integración de Aplicaciones]]
- [[Ciberseguridad como proceso de negocio y NIST CSF 2.0]]
- [[Índice de Seguridad de Integración de Aplicaciones]]

## Fuente

Presentación **Semana 1_Fundamentos de Integración de Aplicaciones.pptx**, 30 diapositivas, revisada en el aula virtual. Contenido reorganizado para estudio; las actividades del proyecto se conservan como material académico.
