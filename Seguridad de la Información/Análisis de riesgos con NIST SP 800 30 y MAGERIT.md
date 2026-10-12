---
tags: [seguridad-informacion, riesgos, nist, magerit]
materia: Seguridad de la Información
unidad: 2
sesion: 6
ciclo: 6to
diapositivas: 22
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546145_1/file/_76033330_1?courseId=_546145_1
---

# Sesión 6: Análisis de riesgos con NIST SP 800-30 y MAGERIT

## 1. Objetivo

Comparar métodos, valorar probabilidad e impacto, calcular ejemplos potencial/residual y comunicar los límites de las estimaciones.

## 2. NIST SP 800-30

Guía para conducir evaluaciones de riesgo, organizar evidencia y priorizar. La sesión la distingue de una norma de certificación.

| Paso | Trabajo |
|---|---|
| Preparar | Alcance, supuestos, restricciones, fuentes y enfoque |
| Conducir | Amenazas, vulnerabilidades, probabilidad, impacto y riesgo |
| Comunicar | Resultados para interesados y decisores |
| Mantener | Revisar cambios en los factores de riesgo |

| Enfoque | Resultado | Límite |
|---|---|---|
| Cualitativo | Muy bajo a muy alto | Ordena; no expresa distancia exacta |
| Semicuantitativo | Rangos numéricos convertidos a etiquetas | Depende de escalas y umbrales |
| Cuantitativo | Pérdida monetaria u otra medida numérica | Exige datos y supuestos sólidos |

Puede priorizarse cualitativamente y cuantificar riesgos críticos. El impacto incluye CIA, operación, finanzas, regulación, reputación y seguridad física.

## 3. MAGERIT v3

Metodología española de análisis y gestión de riesgos de sistemas de información. La presentación la asocia a CCN/PILAR y al ENS y la describe como más prescriptiva. Su afirmación de obligatoriedad debe tratarse como una simplificación docente: el contexto normativo aplicable y la exigencia de una metodología concreta necesitan revisión antes de citarse formalmente.

Tres libros: Método, Catálogo de Elementos y Guía de Técnicas. El modelo estudiado incluye activos, amenazas, vulnerabilidades, salvaguardas, impacto y riesgo.

Cinco dimensiones de valoración: **disponibilidad, integridad, confidencialidad, autenticidad y trazabilidad**. Autenticidad verifica entidad/fuente; trazabilidad permite determinar quién hizo qué y cuándo.

## 4. Potencial y residual

- Potencial: estimación antes de aplicar salvaguardas.
- Residual: estimación considerando las salvaguardas y su eficacia.
- Eficacia en el ejemplo: 0 no protege; 1 protección total modelada. Es un supuesto experto, no una prueba automática.

El material usa PILAR como herramienta de apoyo. Automatizar un cálculo no elimina la necesidad de justificar entradas.

## 5. Ejemplo numérico de la pyme contable

Activo: archivos contables en servidor local. Amenazas: falla de disco o ransomware. Debilidad: ausencia de copias.

| Paso | Cálculo |
|---|---|
| Valor | S/15 000 |
| Degradación | 0,90 |
| Impacto | 15 000 × 0,90 = S/13 500 |
| Frecuencia/probabilidad usada | 0,20 anual, simplificación de una vez cada cinco años |
| Riesgo potencial | 13 500 × 0,20 = S/2 700/año |
| Eficacia backup | 0,85 |
| Degradación residual | 0,90 × (1 − 0,85) = 0,135 |
| Impacto residual | 15 000 × 0,135 = S/2 025 |
| Riesgo residual | 2 025 × 0,20 = S/405/año |

El backup del ejemplo reduce cuánto se pierde; no cambia la frecuencia asignada al ataque. El ahorro esperado modelado es S/2 295/año, antes de costos del control. Esta última diferencia es una derivación aritmética para estudiar el ejemplo.

### El mismo riesgo con tres enfoques

| Enfoque docente | Cálculo | Resultado mostrado |
|---|---|---|
| Cualitativo | Probabilidad moderada × impacto alto | Alto |
| Semicuantitativo | 45 × 70 / 100 | 31,5, moderado en su escala |
| Cuantitativo | S/13 500 × 0,20 | S/2 700/año |

Las etiquetas dependen de la calibración. No convertir 31,5 o «alto» entre métodos sin definir sus criterios. El producto de escalas ordinales es una herramienta de priorización, no una medida monetaria por sí mismo.

## 6. Ejercicio de matriz 5×5

Asignar probabilidad e impacto y justificar: servidor sin parche; envío erróneo de datos; falla eléctrica; exempleado con cuenta activa que cambia nómina; proveedor comprometido; terremoto que afecta dos datacenters en la misma ciudad; credenciales de producción en repositorio público; DDoS en banca; brecha del procesador de pagos; consulta abusiva por soporte.

Una fila completa incluye activo, escenario, dimensiones afectadas, evidencia, probabilidad, impacto, nivel, control y responsable.

## 7. Banco Vallesur

400 000 clientes móviles. El caso combina segundo factor SMS expuesto a SIM swapping con un call center que lo desactiva usando tres preguntas basadas en datos filtrados. Además falta detección temprana frente a una exigencia de reporte de 24 horas planteada por el escenario.

Analizar ambas debilidades y su interacción: reforzar el factor pierde eficacia si recuperación de cuenta lo elude. La respuesta debe incluir detección de cambios de factor, restablecimiento y transacciones anómalas, además de prevención. El plazo de reporte pertenece al caso, no se presenta como una regla legal universal.

## 8. Límites y trabajo final

Dos analistas pueden producir números diferentes por supuestos, evidencia y eficacia asignada. Una cifra con decimales no demuestra certeza. Comunicar estimación, escenario, límites y razones; seleccionar cualitativo o cuantitativo según la decisión que se necesita.

Para el hito, escoger tres a cinco activos críticos y completar su análisis. Inventario sin probabilidad, impacto y nivel queda incompleto. El método hace repetible y defendible el juicio experto.

Apoyo: calculadora NIST/MAGERIT XLSX. Siguiente tema anunciado: tratamiento, apetito y tolerancia con ISO 27005 y SP 800-39. Anterior: [[Fundamentos de riesgos y función Identify de NIST CSF]]. Volver: [[Índice de Seguridad de la Información]].
