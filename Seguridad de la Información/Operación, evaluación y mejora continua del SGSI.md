---
tags: [seguridad-informacion, sgsi, pdca, auditoria]
materia: Seguridad de la Información
unidad: 1
sesion: 4
ciclo: 6to
diapositivas: 17
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546145_1/file/_75819217_1?courseId=_546145_1
---

# Sesión 4: Operación, evaluación y mejora continua del SGSI

## 1. Objetivo

Relacionar cláusulas 7–10 de ISO 27001:2022 con recursos, operación, medición, auditoría y acciones correctivas.

## 2. Cláusula 7: apoyo

| Subcláusula | Evidencia o actividad |
|---|---|
| 7.1 Recursos | Presupuesto, personas y medios necesarios |
| 7.2 Competencia | Educación, formación, experiencia y evaluación |
| 7.3 Conciencia | Conocimiento de política y responsabilidades |
| 7.4 Comunicación | Qué, cuándo, cómo y a quién comunicar |
| 7.5 Información documentada | Creación, actualización y control de documentos |

Actividad «Detective de evidencia»: procedimiento de incidentes que nadie encuentra → documentación; presupuesto de firewall → recursos; empleado que reenvía phishing simulado → conciencia/competencia según causa; boletín del comité → comunicación. La clasificación debe apoyarse en el problema y la evidencia, no solo en palabras clave.

## 3. Cláusula 8: operación

8.1 planifica e implementa procesos y controla cambios. 8.2 evalúa riesgos a intervalos previstos y ante cambios significativos. 8.3 implementa el plan de tratamiento. Las opciones de tratamiento del material son aceptar, mitigar, transferir o evitar.

## 4. PDCA

| Etapa | Aplicación docente | Ejemplo MFA |
|---|---|---|
| Planificar | Riesgos, objetivos y tratamiento, cláusula 6 | Definir objetivo y plan |
| Hacer | Apoyo y operación, 7–8 | Configurar y capacitar |
| Verificar | Evaluación, 9 | Revisar logs, cobertura y configuración |
| Actuar | Mejora, 10 | Corregir omisiones y ajustar política |

Ejercicio: clasificar objetivo de reducir accesos 90%, configurar MFA VPN, revisar logs mensuales, capacitar, detectar 15% sin activar, actualizar política, asignar presupuesto y auditar configuración. El presupuesto forma parte del plan y proporciona recursos para la ejecución; explicar la perspectiva usada.

## 5. Cláusula 9: desempeño

- **9.1:** definir qué medir, método, frecuencia, responsables, análisis y evaluación.
- **9.2:** auditar cumplimiento y eficacia con objetividad e independencia.
- **9.3:** revisión por la alta dirección a intervalos planificados.

ISO/IEC 27004 proporciona guía para diseñar mediciones, líneas base e indicadores. La sesión la vincula a los futuros KPI/KRI del curso. El responsable de un proceso no debe ser su único auditor independiente.

## 6. Caso TransAndina

La política exige capacitación anual a todo el personal operativo. Hay evidencia completa de 60% en los últimos doce meses; operaciones dice que capacita, pero no siempre registra.

Separar:

1. Requisito: capacitación obligatoria y evidencia correspondiente.
2. Evidencia: cobertura demostrada de 60%.
3. Brecha: 40% sin respaldo suficiente.
4. Investigación: ausencia de formación, de registro o ambas.
5. Acción: corregir brecha y causa del proceso, verificar eficacia.

No basta con aceptar una explicación verbal. La severidad se determina por alcance y carácter sistemático del incumplimiento.

| Hallazgo | Significado de uso común presentado |
|---|---|
| No conformidad mayor | Ausencia o falla sistemática de un requisito |
| No conformidad menor | Incumplimiento puntual sin falla del conjunto |
| Observación | Debilidad potencial sin incumplimiento demostrado |
| Oportunidad de mejora | Sugerencia sin incumplimiento |

La presentación aclara que esta clasificación es práctica de auditoría, no texto literal de la cláusula 9.

## 7. Cláusula 10: mejora

10.1 mejora continuamente idoneidad, adecuación y eficacia. 10.2 responde a no conformidades, investiga causas, implementa correcciones/acciones y revisa eficacia.

**Corrección:** resolver el caso actual. **Acción correctiva:** tratar su causa para evitar repetición. Cerrar un ticket sin comprobar eficacia no completa el aprendizaje del SGSI.

## 8. Trabajo, evaluación y repaso

La sesión anuncia PC1. El plan de tratamiento del hito de semana 7 se relaciona con 8.3; hallazgos y causas justifican controles y mejora.

- Reconstruir PDCA con un control real.
- Distinguir medir, auditar y revisar por la dirección.
- Analizar TransAndina sin confundir falta de registro con evidencia de capacitación.
- Proponer una acción correctiva y un indicador de eficacia.

Apoyo: ISO 27004:2016 publicada en el aula. Anterior: [[Contexto, liderazgo y planificación del SGSI]]. Siguiente: [[Fundamentos de riesgos y función Identify de NIST CSF]]. Volver: [[Índice de Seguridad de la Información]].
