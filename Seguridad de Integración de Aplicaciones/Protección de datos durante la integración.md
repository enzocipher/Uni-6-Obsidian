---
tags: [integracion, datos, tls, pki, cifrado, firma-digital]
materia: Seguridad de Integración de Aplicaciones
unidad: 2
sesion: 6
ciclo: 6to
diapositivas: 38
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546137_1/file/_76001836_1?courseId=_546137_1
---

# Sesión 6: Protección de datos durante la integración

## 1. Objetivo

Identificar qué información circula por las integraciones y cómo protegerla. Se reutilizan el catálogo de APIs y el modelo AuthN/AuthZ, con especial atención a las APIs críticas.

Controlar quién accede y qué puede hacer debe complementarse con proteger los datos que se intercambian.

## 2. Tipo y sensibilidad de la información

| Concepto | Pregunta | Ejemplos |
|---|---|---|
| Tipo | ¿Qué clase de información es? | Personal, transaccional, credencial o token, negocio, técnica |
| Sensibilidad | ¿Qué impacto tendría su exposición, alteración o uso indebido? | Pública, interna, confidencial, restringida o crítica |

La organización define su esquema de clasificación. La sensibilidad depende del impacto y del contexto, no únicamente del nombre del dato.

Ejemplo de la sesión: un número de cuenta es información transaccional y puede clasificarse como confidencial. “Transaccional” describe su tipo; “confidencial” expresa el nivel de protección requerido.

## 3. Necesidades de protección

| Propiedad | Necesidad |
|---|---|
| Confidencialidad | Solo los destinatarios correspondientes pueden conocer la información |
| Integridad | La información conserva su contenido frente a modificaciones indebidas |
| Autenticidad | Se puede confiar en el origen de la información o comunicación |

Esta sesión se concentra en esas propiedades durante la integración. La disponibilidad sigue siendo relevante para el proceso, aunque no sea el foco de los mecanismos criptográficos presentados.

## 4. Datos en tránsito y riesgos

Los datos pueden recorrer cliente, API, servicio, core y partner. Debe analizarse cada salto y sus extremos.

| Escenario | Qué sucede | Necesidad principal |
|---|---|---|
| Intercepción | Un tercero observa información que no debería conocer | Confidencialidad |
| Modificación | Se alteran datos durante su recorrido | Integridad |
| Suplantación | La comunicación llega a un servicio que no es el esperado | Autenticidad |
| Exposición | Datos sensibles quedan accesibles indebidamente | Protección de la información según el contexto |

La secuencia de análisis es **riesgo → necesidad de protección → control**. El mecanismo debe responder al problema localizado en un flujo concreto.

## 5. TLS y HTTPS

**TLS**, Transport Layer Security, protege la comunicación entre sus extremos mediante confidencialidad, integridad y autenticación del servidor usando certificados.

**HTTPS es HTTP sobre TLS.** HTTP define la comunicación de aplicación; TLS protege el canal.

Debe identificarse dónde se aplica TLS. Si un recorrido tiene varios saltos, proteger uno no describe automáticamente la protección de los demás.

## 6. Certificados digitales y PKI

Un certificado vincula una identidad con una clave pública. Puede contener sujeto, emisor, clave pública, vigencia y firma del emisor.

La pregunta esencial es por qué se confía en ese vínculo. **PKI**, Public Key Infrastructure, administra autoridades certificadoras, certificados, claves, validación y ciclo de vida.

Cadena ilustrativa de confianza:

```text
Autoridad raíz (Root CA)
    → Autoridad intermedia (Intermediate CA)
        → Certificado del servidor
```

El cliente debe validar el certificado del servidor en el marco de su confianza. Presentar un certificado sin validarlo no completa la decisión de autenticidad.

## 7. Cifrado y firma digital

| Mecanismo | Función principal | Idea de funcionamiento |
|---|---|---|
| Cifrado simétrico | Confidencialidad | Misma clave para cifrar y descifrar |
| Cifrado asimétrico | Confidencialidad según el esquema utilizado | Par de claves pública y privada |
| Firma digital | Integridad y autenticidad del contenido | Firma con clave privada y verificación con clave pública |

La presentación explica la firma mediante documento, hash, firma con clave privada y verificación con la clave pública del emisor. La garantía de no repudio depende del contexto y de condiciones específicas.

Firmar no oculta la información. La elección de mecanismos puede combinar cifrado y firma cuando se requieren confidencialidad e integridad o autenticidad del mensaje.

## 8. Proteger canal y proteger contenido

| Aspecto | Protección del canal | Protección del dato o mensaje |
|---|---|---|
| Objeto | Comunicación entre dos extremos | Contenido intercambiado |
| Ejemplos | TLS y HTTPS | Cifrado y firma digital |
| Alcance | Durante la comunicación protegida | Sobre el contenido, según el mecanismo y sus destinatarios |
| Necesidad | Confidencialidad, integridad y autenticidad del servidor | Confidencialidad o integridad y autenticidad del mensaje |

Son decisiones que pueden complementarse. Una debe explicar el recorrido protegido y la otra qué protección necesita conservar el contenido.

## 9. Matriz de decisión

| API o flujo | Datos | Sensibilidad | Riesgo | Necesidad | Control | Justificación |
|---|---|---|---|---|---|---|
| API Clientes | Datos personales | Alta | Intercepción | Confidencialidad | TLS/HTTPS | Proteger datos durante la comunicación |
| API Pagos | Datos transaccionales | Crítica | Intercepción o modificación | Confidencialidad e integridad | TLS/HTTPS | Limitar exposición y alteración en tránsito |

La justificación debe decir qué se aplica, dónde y qué propiedad protege. El nombre de una herramienta deja esas decisiones incompletas.

### Ejemplo visual: tienda online

La API de pedidos intercambia pedido y datos del cliente con sensibilidad alta. Pedidos envía producto y cantidad hacia inventario con sensibilidad media, e importe y referencia hacia pagos con sensibilidad alta o crítica.

El caso propone HTTPS/TLS para esos flujos. En pagos contempla protección adicional según la necesidad. La matriz debe distinguir datos, sensibilidad, intercepción, alteración o exposición y explicar qué protege cada control.

## 10. Proyecto integrador: avance 6

Para las APIs críticas del catálogo:

1. Identificar API y datos intercambiados.
2. Clasificar su sensibilidad.
3. Describir el riesgo en tránsito.
4. Determinar la propiedad que debe preservarse.
5. Seleccionar el control y su ubicación.
6. Justificar la relación entre datos, riesgo y control.

Entregable: **Controles para Protección de Datos en Tránsito**. Se mantiene coherencia con la arquitectura y el modelo de acceso de la sesión 5.

## 11. Repaso

1. ¿Cómo distinguir tipo de dato y sensibilidad?
2. ¿Por qué AuthN/AuthZ no cubre por sí solo la protección de datos?
3. ¿Qué relación existe entre HTTPS, TLS, certificados y PKI?
4. ¿Por qué una firma no aporta confidencialidad por sí sola?
5. ¿Qué diferencia existe entre proteger un canal y un mensaje?

## Conexiones

- [[Autenticación, autorización y gestión de identidades en APIs]]
- [[Fundamentos de Seguridad de la Información y triada CIA]]
- [[Dinámicas de integración, acceso y protección de datos]]
- [[Índice de Seguridad de Integración de Aplicaciones]]

## Fuente

Presentación **Sesion06_Clase_SIA.pptx**, 38 diapositivas, revisada en el aula virtual. Incluye la reconstrucción textual de la matriz visual del proyecto.
