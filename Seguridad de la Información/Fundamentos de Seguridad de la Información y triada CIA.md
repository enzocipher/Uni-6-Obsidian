---
tags: [seguridad-informacion, fundamentos, cia]
materia: Seguridad de la Información
unidad: 1
sesion: 1
ciclo: 6to
diapositivas: 18
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546145_1/file/_75467400_1?courseId=_546145_1
---

# Sesión 1: Fundamentos de Seguridad de la Información y triada CIA

## 1. Propósito del curso

Diseñar, gobernar y mejorar un programa de Seguridad de la Información alineado al negocio y basado en riesgos. La presentación reúne cuatro ejes: gobierno, riesgos, controles y resiliencia.

| Eje | Contenido |
|---|---|
| Gobierno | Políticas, CISO, comités y responsabilidades |
| Riesgos | Identificación, evaluación y tratamiento |
| Controles | ISO 27001/27002, NIST y CIS |
| Resiliencia | Incidentes, continuidad y métricas |

Ruta de dieciséis semanas: unidad 1, gobierno y marcos, semanas 1–4; unidad 2, ciberriesgos, 5–8; unidad 3, controles y cumplimiento, 9–12; unidad 4, resiliencia, métricas y respuesta, 13–16.

## 2. Seguridad de la Información y Ciberseguridad

El diagrama docente representa Ciberseguridad dentro de Seguridad de la Información.

| Dimensión | Seguridad de la Información | Ciberseguridad |
|---|---|---|
| Foco | Información física, digital y conocimiento | Activos tecnológicos y datos digitales |
| Elementos | Personas, procesos, gobierno y cumplimiento | Redes, endpoints, código y arquitectura |
| Herramientas ejemplificadas | Políticas, riesgo, SGSI, auditoría y cultura | Firewall, EDR, SIEM y pruebas técnicas |

La gestión de seguridad debe considerar cómo se crea, usa y conserva información, incluido el conocimiento de las personas. Los productos técnicos son parte de esa protección.

## 3. Triada CIA

| Propiedad | Definición | Consecuencia de falla |
|---|---|---|
| Confidencialidad | Acceso únicamente por quienes están autorizados | Fuga de datos y sanciones |
| Integridad | Exactitud y ausencia de alteración indebida | Fraude y pérdida de confianza |
| Disponibilidad | Acceso cuando lo requiere el negocio | Parada operativa y pérdida económica |

La letra A procede de *Availability*; en español también se escribe CID. Las tres dimensiones se analizan juntas y según el proceso: una interrupción en un banco durante pagos masivos puede tener impacto crítico.

## 4. Caso ChasquiPay

La superapp del ejercicio procesa 50 000 transacciones por hora, tiene dos millones de usuarios y expone S/150 000 de ingresos por hora de inactividad. En hora punta, el SOC detecta un atacante que superó el perímetro e intenta escalar privilegios hacia tarjetas y saldos. El escenario indica que aún no ha extraído los datos.

| Perspectiva | Prioridad | Postura del ejercicio |
|---|---|---|
| CISO | Confidencialidad | Parar bases de datos para evitar extracción y daño legal/reputacional |
| COO | Disponibilidad | Mantener servicio por el impacto en pagos, comercios y repartidores |
| Auditor | Integridad | Congelar transacciones para impedir alteración de saldos |

El ejercicio pide defender una decisión frente a estas consecuencias. Las posturas son roles del caso, no una solución técnica ya aprobada. Una respuesta debe identificar activos, impacto de cada opción, alcance de contención y criterios para recuperar el servicio.

## 5. Trabajo Final Integrado

**Semana 7, TP1:** entorno organizacional y activos críticos; análisis NIST SP 800-30/MAGERIT; tratamiento inicial; controles ISO/CIS.

**Semana 15, TF1 + DD1:** gobierno del SGSI, roles y políticas; cumplimiento legal citado en el material, incluyendo Ley 29733 y GDPR; incidentes y continuidad/BIA; métricas ejecutivas y roadmap de doce meses. Las referencias legales son contenido docente, no evaluación de aplicabilidad a una organización concreta.

## 6. Repaso

- Explicar por qué una política y un control de endpoint pertenecen a niveles distintos del programa.
- Dar un ejemplo de falla por cada propiedad CIA.
- Defender una decisión en ChasquiPay sin ignorar las otras dos dimensiones.
- Relacionar gobierno, riesgo, controles y resiliencia con el trabajo final.

Material de apoyo publicado: NIST SP 800-12 Rev. 1. Siguiente: [[Gobierno de TI, rol del CISO y familia ISO 27000]]. Volver: [[Índice de Seguridad de la Información]].
