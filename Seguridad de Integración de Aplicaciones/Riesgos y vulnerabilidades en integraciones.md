---
tags: [integracion, riesgos, vulnerabilidades, activos, cia]
materia: Seguridad de Integración de Aplicaciones
unidad: 1
sesion: 3
ciclo: 6to
diapositivas: 32
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546137_1/file/_75777659_1?courseId=_546137_1
---

# Sesión 3: Riesgos y vulnerabilidades en integraciones

## 1. Objetivo

Leer una arquitectura de integración para identificar sus principales riesgos. El análisis continúa sobre el mismo escenario: inventario y ecosistema de la sesión 1, AS-IS de la sesión 2 y vista de riesgos de la sesión 3.

Una integración puede funcionar y seguir expuesta. La validación funcional no necesariamente revela permisos excesivos, datos sensibles, confianza mal delimitada o dependencias críticas.

## 2. Cinco elementos que observar

| Elemento | Pregunta |
|---|---|
| Componentes | ¿Qué sistemas y servicios existen? |
| Conexiones | ¿Cómo se comunican? |
| Datos | ¿Qué información circula? |
| Actores | ¿Quién accede o participa? |
| Dependencias | ¿De quién depende el proceso? |

El análisis debe localizarse en componentes o flujos concretos del AS-IS. Un riesgo genérico sin relación con la arquitectura no permite justificar un cambio.

## 3. Construcción de un escenario de riesgo

| Concepto | Definición | Ejemplo |
|---|---|---|
| Activo | Elemento valioso que necesita protección | Datos personales de clientes |
| Amenaza | Fuente o circunstancia con capacidad potencial de daño | Atacante externo |
| Vulnerabilidad | Debilidad que facilita un efecto adverso | Servicio expuesto inadecuadamente |
| Riesgo | Escenario adverso que podría ocurrir | Acceso no autorizado a información de clientes |
| Impacto | Consecuencia del escenario | Exposición de información sensible |

Una amenaza puede ser un atacante, usuario interno, proveedor, malware, error humano o falla tecnológica. Una vulnerabilidad puede ser configuración insegura, permisos excesivos, credenciales débiles, software desactualizado, exposición innecesaria o diseño inadecuado.

**Activo, amenaza, vulnerabilidad y riesgo son conceptos distintos.** Una condición como “dependemos de un tercero” debe desarrollarse hasta explicar qué evento podría ocurrir y qué consecuencia tendría.

## 4. Criticidad del activo

La criticidad se determina por lo que sucedería si el activo se expone, se modifica o deja de estar disponible. En la presentación aparecen portal público, datos de clientes, servicio de pagos y credenciales administrativas como ejemplos de impactos crecientes.

Estas clasificaciones son ilustrativas. La misma API puede ser crítica en un proceso y tener otro nivel en otro contexto. Deben justificarse las consecuencias para la organización.

## 5. Superficie de ataque y límites de confianza

La **superficie de ataque** reúne los puntos por los cuales un sistema puede ser alcanzado o interactuado: APIs, interfaces, servicios, usuarios, terceros, cloud y datos expuestos.

Un **límite de confianza** aparece donde cambia el contexto en el que se confía en un participante o intercambio. La interacción entre una aplicación y un tercero merece atención especial por sus responsabilidades y controles distintos.

Para cada conexión:

1. ¿Qué información circula?
2. ¿Quién la origina y quién la consume?
3. ¿Atraviesa un límite de confianza?
4. ¿De qué componente depende?
5. ¿Qué ocurre si ese componente o flujo se compromete?

Una flecha representa datos, participantes, confianza y dependencia. Externalizar una capacidad conserva la necesidad de gestionar el riesgo que introduce en el proceso.

## 6. CIA e impacto empresarial

| Propiedad | Pregunta de análisis |
|---|---|
| Confidencialidad | ¿Quién puede conocer la información? |
| Integridad | ¿Quién puede modificarla? |
| Disponibilidad | ¿Qué ocurre si deja de estar accesible? |

Un riesgo puede afectar varias propiedades. La consecuencia técnica debe traducirse a una consecuencia para el negocio: interrupción de compras, exposición de clientes, demora operativa o pérdida de confianza, según el escenario.

## 7. Priorización

La sesión relaciona **probabilidad e impacto** para asignar prioridad. La siguiente matriz reproduce la escala cualitativa de la presentación:

| Impacto / Probabilidad | Baja | Media | Alta |
|---|---|---|---|
| Alto | Medio | Alto | Crítico |
| Medio | Bajo | Medio | Alto |
| Bajo | Bajo | Bajo | Medio |

Crítico implica atención inmediata; alto, atención alta; medio, atención moderada; bajo, atención baja. Es una matriz de clase, cuyos criterios deben acordarse al aplicarla a una organización.

## 8. Registro inicial de riesgos

| ID | Integración o componente | Activo | Escenario | Impacto | Probabilidad |
|---|---|---|---|---|---|
| R01 | API Clientes | Datos personales | Acceso no autorizado | Alto | Media |
| R02 | Pagos | Transacciones | Interrupción del servicio | Alto | Media |
| R03 | Proveedor | Servicio crítico | Falla del tercero | Medio | Baja |

El diagrama y la matriz deben describir la misma realidad. Los identificadores permiten volver desde un riesgo al componente o flujo afectado.

## 9. Proyecto integrador: avance 3

1. Recuperar los dos procesos del laboratorio 2 y su AS-IS.
2. Identificar activos, exposición y dependencias.
3. Incorporar tres pistas o condiciones nuevas.
4. Determinar si cada pista afecta uno, ambos o ninguno de los procesos; justificar la conclusión.
5. Documentar riesgos, impacto y probabilidad.

**Tres pistas no equivalen a tres riesgos.** Una pista puede dar lugar a varios escenarios o no afectar el proceso analizado. La matriz inicial debe incluir ID, integración o componente, activo, escenario, impacto y probabilidad.

### Ejemplo visual: tienda online

El recorrido pasa por cliente, web o app, API Gateway, pedidos, pagos y proveedor externo. Se informa que el proveedor de pagos presenta interrupciones recurrentes durante alta demanda.

- **Activo:** servicio o proceso de pago.
- **Dependencia:** proveedor externo de pagos.
- **Situación:** indisponibilidad del proveedor.
- **Riesgo:** no completar compras cuando el servicio externo no está disponible.
- **Impacto:** alto, porque puede detener ventas.
- **Probabilidad:** debe justificarse con la información del caso; el ejemplo la deja para el análisis.

Los riesgos serán la entrada para construir el TO-BE en la siguiente sesión.

## 10. Repaso

1. ¿Por qué funcionar correctamente no demuestra ausencia de riesgo?
2. ¿Cómo convertir una condición en un escenario?
3. ¿Qué revela un límite de confianza?
4. ¿Cómo relacionar un riesgo con CIA y con el negocio?
5. ¿Qué evidencia permite justificar su prioridad?

## Conexiones

- [[Arquitecturas y patrones de Integración de Aplicaciones]]
- [[Security by Design y arquitectura TO BE]]
- [[Fundamentos de riesgos y función Identify de NIST CSF]]
- [[Dinámicas de integración, acceso y protección de datos]]
- [[Índice de Seguridad de Integración de Aplicaciones]]

## Fuente

Presentación **Sesion03_Clase_SIA_Riesgos y Vulnerabilidades en Integraciones.pdf**, 32 diapositivas, revisada en el aula virtual. Se conserva la matriz cualitativa y se describe el caso visual de tienda online.
