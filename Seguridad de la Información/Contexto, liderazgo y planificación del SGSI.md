---
tags: [seguridad-informacion, sgsi, iso27001, soa]
materia: Seguridad de la Información
unidad: 1
sesion: 3
ciclo: 6to
diapositivas: 21
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546145_1/file/_75768753_1?courseId=_546145_1
---

# Sesión 3: Contexto, liderazgo y planificación del SGSI

## 1. Objetivo

Aplicar las cláusulas 4, 5 y 6 de ISO/IEC 27001:2022 a la organización del trabajo: contexto, interesados, alcance, liderazgo y planificación.

## 2. Vocabulario de riesgo

| Término | Definición | Ejemplo |
|---|---|---|
| Activo | Elemento valioso que requiere protección | Base de clientes |
| Amenaza | Causa potencial de incidente | Ransomware |
| Vulnerabilidad | Debilidad explotable | Software sin parches |
| Riesgo | Escenario de amenaza, debilidad y consecuencia sobre el activo | Cifrado del servidor al explotar software sin parchear |

La amenaza no es la debilidad propia. Un riesgo se redacta como escenario, con consecuencia, y se evalúa según los criterios del SGSI.

## 3. Qué es un SGSI

Conjunto de políticas, procedimientos, roles, controles y procesos para gestionar seguridad de forma sistemática y repetible. Su diseño depende de la organización y de sus riesgos.

## 4. Cláusula 4: contexto

| Subcláusula | Pregunta práctica |
|---|---|
| 4.1 Organización y contexto | ¿Qué factores internos/externos influyen: cultura, estructura, mercado y regulación? |
| 4.2 Partes interesadas | ¿Quién espera qué en seguridad? |
| 4.3 Alcance | ¿Qué incluye el SGSI, qué interfaces existen y cómo se justifica? |
| 4.4 Sistema | ¿Qué procesos e interacciones necesita? |

Orden de trabajo: contexto → requisitos de interesados → alcance → procesos.

### Partes interesadas

Internas: directorio, empleados, comité, CISO/CIO. Externas: clientes, reguladores, proveedores, accionistas y aseguradoras.

Para cada una: **requisito concreto + consecuencia de incumplimiento**. Por ejemplo, clientes esperan protección de datos; dirección necesita informes de riesgo; proveedor necesita responsabilidades claras. El material cita SBS y Ley 29733 como ejemplos de requisitos que dependen del sector y organización.

Actividad: identificar tres partes internas y tres externas con un requisito específico por cada una.

### Caso de alcance

Banco con tres sedes, centro de datos y call center tercerizado que accede a datos de clientes. La externalización no elimina la dependencia: el acceso y proceso deben considerarse al definir alcance y controles de proveedor.

El documento muestra ejemplos de exclusión de marketing, oficinas o un call center completamente aislado. No son exclusiones automáticas: deben justificarse por los límites e interfaces reales. Excluir por conveniencia un servicio que procesa datos críticos deja una brecha.

## 5. Cláusula 5: liderazgo

- **5.1:** demostrar compromiso de la alta dirección.
- **5.2:** aprobar, comunicar y poner a disposición la política.
- **5.3:** asignar responsabilidades y autoridad de forma clara.

Firmar una política es una evidencia posible; también deben existir decisiones, recursos y supervisión que sostengan el sistema.

## 6. Cláusula 6: planificación

6.1 trata riesgos y oportunidades, evaluación y tratamiento. 6.2 exige objetivos de seguridad medibles, comunicados y planificados.

La SoA conecta decisiones de tratamiento con controles. Debe justificar inclusión/exclusión y reflejar estado de implementación; la tabla del curso simplifica la estructura a control, aplica y justificación.

| Ejemplo docente | Decisión | Justificación mostrada |
|---|---|---|
| 8.7 Malware | Sí | Riesgo de ransomware |
| 7.4 Monitoreo físico | No | Infraestructura alojada en Cloud |
| 5.23 Nube | Sí | Servicios críticos en proveedor Cloud |

La segunda fila requiere análisis: estar en Cloud no elimina por sí solo toda necesidad de protección física en oficinas o equipos. La SoA debe corresponder al alcance concreto.

## 7. Riesgo estratégico y operativo

Estratégico: afecta reputación, dirección o viabilidad de largo plazo. Operativo: afecta procesos diarios. Un incidente puede tener ambas dimensiones; la dirección decide prioridades y la gestión ejecuta su tratamiento.

Ejercicio: clasificar servidor caído dos horas, fuga que destruye confianza y sanción que amenaza licencia, explicando contexto y alcance del impacto.

## 8. Entregable y repaso

El hito de semana 7 incorpora interesados, alcance y justificaciones. Elaborar el borrador a partir de activos y procesos, no de una lista de controles genérica.

- Redactar un riesgo completo.
- Explicar requisitos e impacto de una parte interesada.
- Justificar inclusión de un tercero.
- Relacionar liderazgo, objetivos, tratamiento y SoA.

Fuente de apoyo: ISO/IEC 27001:2022 publicada en el aula. Anterior: [[Gobierno de TI, rol del CISO y familia ISO 27000]]. Siguiente: [[Operación, evaluación y mejora continua del SGSI]]. Volver: [[Índice de Seguridad de la Información]].
