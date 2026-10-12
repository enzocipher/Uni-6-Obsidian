---
tags: [integracion, security-by-design, arquitectura, to-be]
materia: Seguridad de Integración de Aplicaciones
unidad: 1
sesion: 4
ciclo: 6to
diapositivas: 33
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546137_1/file/_75809592_1?courseId=_546137_1
---

# Sesión 4: Security by Design y arquitectura TO-BE

## 1. Objetivo

Transformar riesgos en decisiones arquitectónicas justificadas. **Security by Design** incorpora seguridad desde las primeras decisiones de diseño: comprender riesgos, diseñar considerando seguridad, construir y validar.

El análisis sigue esta cadena:

**Riesgo → principio → decisión → cambio en el TO-BE → efecto esperado.**

Antes de agregar herramientas, se revisa si el diseño puede eliminar una exposición, reducir una dependencia o limitar el alcance de una falla.

## 2. AS-IS y TO-BE

| Vista | Qué representa |
|---|---|
| AS-IS | Arquitectura actual y funcionamiento conocido |
| TO-BE | Evolución propuesta, sustentada en necesidades y riesgos |

El TO-BE debe permitir observar qué se mantiene, modifica, elimina o incorpora. Su valor depende de la relación entre el cambio y el problema que intenta resolver.

## 3. Preguntas iniciales de diseño

- ¿Necesitamos esta conexión?
- ¿Necesitamos exponer este componente?
- ¿Necesitamos compartir estos datos?
- ¿Necesitamos este nivel de acceso?
- ¿Necesitamos esta dependencia?

Responder estas preguntas puede reducir riesgo antes de seleccionar mecanismos tecnológicos.

## 4. Principios de diseño seguro

| Principio | Aplicación al diseño | Pregunta |
|---|---|---|
| Security by Default | Estado inicial razonablemente seguro, con acceso restringido | ¿La arquitectura parte de una posición segura? |
| Mínimo privilegio | Cada usuario, servicio o componente obtiene solo lo necesario | ¿Necesita leer, escribir, eliminar o administrar? |
| Separación de responsabilidades | Delimitar funciones y accesos | ¿Estamos concentrando demasiadas responsabilidades? |
| Reducción de superficie de ataque | Retirar exposición e interacciones innecesarias | ¿Se necesita realmente esta API o interfaz? |
| Simplicidad | Evitar complejidad que dificulta proteger y operar | ¿Existe una forma más simple de resolverlo? |
| Defensa en profundidad | Combinar prevención, detección, respuesta y recuperación | ¿Qué limita el daño si falla una protección? |

Necesitar leer un recurso no justifica disponer de permisos de modificación, eliminación o administración. Un componente que hace todo, accede a todo y controla todo concentra riesgo.

Los principios ayudan a razonar. Una decisión puede aplicar varios a la vez: eliminar una integración innecesaria reduce exposición, simplifica la arquitectura y retira una dependencia.

## 5. Convertir riesgos en decisiones

Ante una dependencia o exposición se puede evaluar:

1. **Eliminar:** ¿hay una alternativa que evite esa dependencia?
2. **Reducir:** ¿puede utilizarse un alcance menor?
3. **Aislar:** ¿puede contenerse para limitar su propagación?
4. **Limitar el impacto:** ¿cómo se mantiene o recupera el proceso si falla?

| Riesgo | Principio | Decisión de diseño | Efecto esperado |
|---|---|---|---|
| R01: exposición innecesaria | Reducir superficie | Eliminar una interfaz sin necesidad de negocio | Menor exposición |
| R02: acceso excesivo | Mínimo privilegio | Delimitar responsabilidad y acceso | Menor alcance de uso indebido |
| R03: dependencia externa crítica | Separación de responsabilidades | Aislar la integración externa | Menor propagación de sus efectos |

La matriz explica por qué existe cada cambio del diagrama. Nombrar un principio sin explicar su aplicación deja incompleta la decisión.

## 6. Alcance del diseño y de los controles

Algunos riesgos se eliminan desde la arquitectura; otros se reducen parcialmente y requieren controles de autenticación, autorización, protección de datos, seguridad de APIs o monitoreo.

Security by Design prepara una arquitectura en la que esos controles responden a necesidades identificadas. Un rediseño debe declarar su efecto esperado y reconocer lo que queda pendiente de controlar.

## 7. Qué mostrar en el TO-BE v1

- Componentes propuestos y responsabilidades.
- Integraciones necesarias.
- Dependencias externas.
- Límites de confianza.
- Cambios respecto del AS-IS.
- Relación entre riesgo, principio, decisión y efecto esperado.

Una propuesta puede mejorar al retirar componentes o conexiones. El número de tecnologías añadidas no es un criterio suficiente de calidad.

## 8. Caso visual: tienda online

El AS-IS depende directamente de un proveedor externo de pagos para completar compras. El riesgo identificado es no completar la compra cuando el proveedor no está disponible.

La propuesta de la presentación introduce un **servicio propio de pagos** con registro o estado de pagos y aísla la comunicación con el proveedor mediante una API. Mantiene cliente, web o app, API Gateway y pedidos.

| Aspecto | Explicación |
|---|---|
| Principio | Separar responsabilidades y limitar el impacto |
| Decisión | Aislar la integración con el proveedor de pagos |
| Cambio | Concentrar esa dependencia en un componente propio |
| Efecto esperado | Reducir el efecto de la indisponibilidad sobre el resto del proceso |
| Se mantiene | El proceso de compra y las necesidades del negocio |
| Contrapartidas | Mayor complejidad operativa, capacidad de monitoreo propio y posible incremento de costos |

La propuesta es un diseño preliminar. Aislar la integración por sí solo no demuestra continuidad del pago: los mecanismos concretos y el comportamiento ante falla deben definirse en el diseño completo.

## 9. Proyecto integrador: avance 4

1. Recuperar AS-IS y riesgos del laboratorio 3.
2. Priorizar los riesgos que justifican un cambio.
3. Documentar riesgo, principio y decisión.
4. Construir el TO-BE.
5. Explicar qué cambió, por qué y qué efecto se espera.

Todo cambio relevante debe justificarse. La entrega incluye el diagrama y su sustento; algunos riesgos pueden requerir controles sin modificar la arquitectura.

## 10. Repaso

1. ¿Cómo distinguir Security by Design de Security by Default?
2. ¿Qué diferencia existe entre aislar y eliminar una dependencia?
3. ¿Qué riesgo reduce cada cambio del TO-BE?
4. ¿Qué costo o complejidad introduce la decisión?
5. ¿Qué queda pendiente de proteger mediante controles?

## Conexiones

- [[Riesgos y vulnerabilidades en integraciones]]
- [[Autenticación, autorización y gestión de identidades en APIs]]
- [[Defensa en Profundidad y Zero Trust]]
- [[Dinámicas de integración, acceso y protección de datos]]
- [[Índice de Seguridad de Integración de Aplicaciones]]

## Fuente

Presentación **Sesion04_Security by Design.pdf**, 33 diapositivas, revisada en el aula virtual. El caso de tienda online se reconstruye a partir del ejemplo visual. La observación sobre continuidad delimita lo que demuestra el diseño preliminar.
