---
tags: [arquitectura, ciberseguridad, negocio, madurez]
materia: Arquitectura de Ciberseguridad
unidad: 1
sesion: 1
ciclo: 6to
diapositivas: 33
actualizado: 2026-10-11
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546141_1/file/_75558805_1?courseId=_546141_1
---

# Sesión 1: Introducción a la Arquitectura de Ciberseguridad

## 1. Objetivo

Comprender la arquitectura de ciberseguridad, su relación con la arquitectura empresarial y el rol del arquitecto. El resultado práctico es diagnosticar la madurez de una organización frente a sus riesgos.

Esta nota completa la sesión introductoria que faltaba en el proyecto. La fuente contiene 33 diapositivas y se revisó el 11 de octubre de 2026.

## 2. Concepto de arquitectura de ciberseguridad

Conjunto de principios, modelos, políticas y estándares que define cómo se estructuran e integran los controles de seguridad, en relación con los objetivos del negocio y su apetito de riesgo.

La arquitectura establece qué se debe proteger, por qué y con qué estructura. Produce decisiones que guían la construcción y la operación:

- Diseña estructuras, estándares y controles antes de adquirir o construir tecnología.
- Relaciona la seguridad con las prioridades estratégicas y el riesgo aceptable.
- Mantiene una orientación de largo plazo y facilita decisiones consistentes.

## 3. Arquitectura y seguridad operativa

| Dimensión | Arquitectura | Operación |
|---|---|---|
| Horizonte ilustrativo | Estratégico, de 3 a 5 años | Táctico y diario |
| Enfoque | Diseño de controles y estándares | Ejecución y mantenimiento |
| Pregunta | ¿Cómo debe estructurarse la seguridad? | ¿Funcionan hoy los controles? |
| Ejemplo | Definir un estándar de segmentación | Configurar y monitorear un firewall |
| Productos | Modelos, políticas y roadmaps | Alertas, tickets y reportes |

La operación ejecuta el diseño y aporta evidencia para mejorarlo. Una arquitectura documentada necesita aplicación y mantenimiento; una operación sin criterios comunes puede producir soluciones aisladas.

## 4. Evolución y objetivos

La sesión presenta una evolución simplificada: protección perimetral, defensa en capas, alineamiento con el negocio y confianza continua. Los periodos son una explicación docente de la evolución de la disciplina.

| Objetivo | Resultado buscado |
|---|---|
| Reducir riesgo estructural | Corregir debilidades del diseño |
| Alinear seguridad y negocio | Traducir estrategia en requisitos |
| Dar consistencia | Estandarizar la protección entre áreas |
| Permitir escalabilidad | Acompañar el crecimiento del negocio |
| Soportar cumplimiento | Producir controles y evidencia demostrables |
| Optimizar inversión | Priorizar activos e impactos relevantes |

La seguridad puede facilitar nuevos productos, adopción de nube y contratos que exigen garantías. El business case relaciona reducción de riesgo, eficiencia operativa y las iniciativas que se podrán realizar.

### Cifras y ejemplos de contexto

La presentación usa el incidente de Maersk/Petya como motivación y cita noticias sobre la afectación logística. También atribuye a un informe IBM de 2026 un costo promedio global de filtración de US$ 4.99 millones, un aumento del 12% y un incremento del 56% de ataques impulsados por IA.

Estas cifras se conservan como afirmaciones del material docente, sin verificación independiente. No se utilizan como datos confirmados para cálculos del proyecto.

## 5. Relación con la arquitectura empresarial

| Dominio empresarial | Qué describe | Pregunta de seguridad |
|---|---|---|
| Negocio | Procesos, estrategia y modelo operativo | ¿Qué resultado y qué continuidad deben protegerse? |
| Datos | Información y flujos críticos | ¿Qué exposición o alteración tendría mayor impacto? |
| Aplicaciones | Sistemas y servicios | ¿Qué controles y dependencias necesita cada servicio? |
| Tecnología | Infraestructura, redes y nube | ¿Cómo se distribuyen y aplican las protecciones? |

La seguridad es transversal a esos dominios. Utiliza artefactos compatibles con la arquitectura empresarial: modelos, catálogos y roadmaps.

El material menciona la Ley peruana 29733 y sectores con exigencias particulares: banca, salud y gobierno. La formalidad de la arquitectura debe responder al contexto y producir evidencia de sus controles. La diapositiva constituye contexto del curso, no un análisis completo de obligaciones vigentes.

## 6. Rol del arquitecto

El arquitecto traduce riesgo en requisitos y requisitos en diseño. Entre sus responsabilidades están:

1. Definir estándares, patrones de referencia y guías de diseño seguro.
2. Evaluar riesgos de proyectos e iniciativas tecnológicas.
3. Diseñar y revisar controles para sistemas, redes y aplicaciones.
4. Revisar decisiones técnicas desde la perspectiva de seguridad.
5. Convertir el apetito de riesgo del negocio en requisitos técnicos.
6. Apoyar auditoría, cumplimiento y equipos de TI o seguridad.

| Rol | Función principal | Lenguaje de trabajo |
|---|---|---|
| CISO / gobierno | Estrategia, prioridades y decisiones de riesgo | Negocio y riesgo |
| Arquitecto | Estructura y diseño de la protección | Negocio y tecnología |
| Ingeniero o especialista | Operación, detección y respuesta | Técnico y operativo |

Las líneas de reporte de la diapositiva son ilustrativas; cada organización define su estructura. El arquitecto coordina con negocio, infraestructura y desarrollo, incluyendo seguridad en el ciclo de vida del software.

## 7. Habilidades, especializaciones y artefactos

Las habilidades destacadas son comunicación ejecutiva, pensamiento sistémico, negociación, documentación clara y comprensión de la operación del negocio.

Errores frecuentes: diseñar sin comprender procesos, añadir complejidad innecesaria, ignorar costos o usabilidad, omitir el razonamiento de una decisión y copiar diseños sin adaptarlos.

| Artefacto | Contenido |
|---|---|
| Diagrama de referencia | Estructura de componentes y controles |
| Estándar técnico | Reglas obligatorias dentro de la organización |
| ADR | Contexto, decisión, alternativas y consecuencias |
| Roadmap | Evolución priorizada por riesgo; el ejemplo propone de 1 a 3 años |

La sesión reconoce especializaciones empresariales, de identidad, redes, nube y aplicaciones/DevSecOps. Menciona SABSA, CISSP, TOGAF, CCSP y SC-100 como referencias profesionales del docente.

## 8. Madurez de arquitectura

Escala docente simplificada:

| Nivel | Característica |
|---|---|
| 1. Ad hoc | Decisiones aisladas y respuesta reactiva |
| 2. Definida | Políticas documentadas con aplicación desigual |
| 3. Gestionada | Estándares consistentes y gobierno |
| 4. Optimizada | Mejora continua y anticipación del riesgo |

El diagnóstico exige evidencia sobre decisiones y controles. No se asigna madurez por la cantidad de herramientas instaladas.

## 9. Caso guiado: TechRetail Perú y FinSecure Bank

Son organizaciones ficticias. TechRetail tiene 1,200 colaboradores, 45 tiendas y tres sedes, con seguridad reactiva y sin estándares comunes. Una fuga afecta su sistema de fidelización. FinSecure tiene 1,500 colaboradores, arquitectura basada en SABSA, comité de cambios y roadmap de tres años; contiene un fraude con controles previstos en el diseño.

| Criterio | TechRetail | FinSecure |
|---|---|---|
| Gobierno | Decisiones dispersas por gerencia | Comité revisa cambios relevantes |
| Consistencia | Protección distinta en cada tienda | Estándares comunes entre canales |
| Respuesta | Detecta la fuga después del evento | Contiene el fraude con controles diseñados |
| Escalabilidad | Cada nuevo canal agrega riesgo sin coordinación | Roadmap anticipa crecimiento |
| Costo y beneficio | Inversión reactiva en remediación | Inversión planificada por riesgo |
| Cumplimiento | Evidencia técnica incompleta | Evidencia trazable a estándares y cambios |

Actividad: cuadro comparativo y tres recomendaciones para TechRetail. La tabla reproduce el modelo del docente; otras clasificaciones requieren sustento.

## 10. Caso grupal: Hospital Vida Salud y Grupo Asegurador Confianza

Hospital Vida Salud tiene 450 empleados, carece de equipo de seguridad y sufre ransomware que cifra historias clínicas durante tres días. Confianza tiene 900 empleados y arquitectura apoyada en NIST CSF e ISO 27001.

La consigna solicita comparar los seis criterios anteriores, explicar el impacto del ransomware desde la arquitectura y proponer tres recomendaciones priorizadas. La entrega académica sugerida es un informe de dos a tres páginas o una exposición de cinco a ocho minutos. El material deja la resolución al grupo.

## 11. Recorrido del curso y repaso

| Unidad | Semanas | Enfoque |
|---|---|---|
| 1 | 1 a 4 | Fundamentos, riesgo, defensa en profundidad y Zero Trust |
| 2 | 5 a 8 | Segmentación, ZTNA, SASE, firewalls e IAM |
| 3 | 9 a 12 | Datos, dispositivos, nube y aplicaciones |
| 4 | 13 a 16 | Gobierno, threat modeling y resiliencia |

Preguntas de estudio:

1. ¿Cómo se relaciona una decisión arquitectónica con el apetito de riesgo?
2. ¿Qué evidencia distingue arquitectura definida de gestionada?
3. ¿Qué parte del riesgo debe explicar un ADR?
4. ¿Cómo se reparten las funciones entre CISO, arquitecto y operación?
5. ¿Qué recomendación de TechRetail tendría mayor prioridad y por qué?

## Conexiones

- [[Frameworks de arquitectura de seguridad]]
- [[Gestión de riesgos en arquitectura de seguridad]]
- [[Gobierno de TI, rol del CISO y familia ISO 27000]]
- [[Fundamentos de Integración de Aplicaciones]]
- [[Índice de Arquitectura de Ciberseguridad]]

## Fuente

**Sesion1_Introduccion_Arquitectura_Ciberseguridad va sm.pdf**, 33 diapositivas, vista previa del aula virtual. Se consolidan secciones repetidas y se conservan los casos y consignas como contenido de estudio.
