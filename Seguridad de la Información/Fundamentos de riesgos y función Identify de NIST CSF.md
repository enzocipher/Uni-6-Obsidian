---
tags: [seguridad-informacion, riesgos, nist-csf, identify]
materia: Seguridad de la Información
unidad: 2
sesion: 5
ciclo: 6to
diapositivas: 17
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546145_1/file/_75920800_1?courseId=_546145_1
---

# Sesión 5: Fundamentos de riesgos y función Identify de NIST CSF

## 1. Objetivo

Identificar activos, amenazas, vulnerabilidades e impactos, relacionarlos con Identify y distinguir síntomas de causas que deben mejorarse.

## 2. Escenario de riesgo e impacto

Activo: elemento valioso. Amenaza: causa potencial de incidente. Vulnerabilidad: debilidad explotable. Riesgo: escenario donde una amenaza afecta al activo aprovechando una debilidad. Impacto: magnitud del daño si ocurre.

| Impacto | Ejemplos |
|---|---|
| Financiero | Pérdidas, recuperación, multas |
| Operativo | Interrupción de procesos o servicios |
| Reputacional | Pérdida de confianza |
| Legal/regulatorio | Demandas, sanciones e incumplimiento |

Probabilidad e impacto forman los dos ejes de la matriz. La valoración debe corresponder a criterios definidos para la organización.

## 3. Panorama de NIST CSF 2.0

| Función | Categorías presentadas |
|---|---|
| Govern, 6 | Contexto, estrategia de riesgo, roles, política, supervisión y suministro |
| Identify, 3 | Activos, evaluación de riesgos y mejora |
| Protect, 5 | Identidad/acceso, conciencia, datos, plataforma y resiliencia |
| Detect, 2 | Monitoreo y análisis de eventos |
| Respond, 4 | Gestión, análisis, reporte/comunicación y mitigación |
| Recover, 2 | Ejecución de recuperación y comunicación |

Govern informa la implementación de las otras funciones. CSF organiza resultados y puede coexistir con el SGSI de ISO 27001.

## 4. Identify

- **ID.AM, Asset Management:** identificar y gestionar activos según su importancia.
- **ID.RA, Risk Assessment:** amenazas, vulnerabilidades, impacto, probabilidad y priorización.
- **ID.IM, Improvement:** mejoras que surgen de evaluación y operación; en la sesión se enfatiza mejorar el proceso de identificación de activos y riesgos.

## 5. Hotelera Costa Azul

Cinco hoteles, reservas con tarjetas, Wi-Fi de huéspedes, kioscos, laptops y PBX conectada a Internet. Ejercicio inicial: identificar cinco activos concretos y una amenaza por cada uno.

| Activo posible del escenario | Valor que se debe explicar |
|---|---|
| Datos de tarjeta en reservas | Protección del huésped y pagos |
| Servicio de reservas | Ingresos y continuidad |
| Kioscos de check-in | Identidad y operación de recepción |
| Laptops administrativas | Acceso a sistemas y datos |
| PBX | Comunicaciones del hotel |

### Incidente resuelto por el material

Un huésped reporta cargos no autorizados. La investigación del caso descubre Wi-Fi público y reservas en el mismo segmento.

- Activo: tarjetas en reservas.
- Amenaza: atacante conectado a Wi-Fi público.
- Vulnerabilidad: falta de separación de redes.
- Riesgo: movimiento lateral desde la red pública hacia tarjetas.
- Síntoma: cargos reportados.
- Causa de diseño: la arquitectura no separó redes con necesidades diferentes.
- Mejora: revisar el patrón en toda la cadena y el proceso de identificación/diseño.

Reembolsar al huésped atiende una consecuencia; corregir la arquitectura trata la causa del escenario.

## 6. Discusión de aceptabilidad

El documento compara: impresora con clave default; equipo hospitalario cuyo parche requiere seis horas de parada; banco que rechaza un control por costo; fintech sin MFA por precio; sistema municipal sin soporte; startup sin cifrado de laptops que contienen código.

Para decidir, explicar activo, impacto, exposición, alternativas, responsable y criterio de aceptación. Ausencia de incidentes anteriores no basta como criterio. Apetito y tolerancia se anuncian para la sesión siguiente.

## 7. Trabajo y repaso

El hito de semana 7 necesita inventario y amenazas, más razones para tratar o aceptar. Evitar activos genéricos como «la base de datos» sin contenido, uso y valor.

- Redactar un riesgo con sus tres elementos y consecuencia.
- Clasificar los cuatro impactos.
- Distinguir ID.AM, ID.RA e ID.IM.
- Explicar síntoma, causa y mejora del hotel.

Apoyo: NIST CSWP 29, CSF 2.0. Anterior: [[Operación, evaluación y mejora continua del SGSI]]. Siguiente: [[Análisis de riesgos con NIST SP 800 30 y MAGERIT]]. Volver: [[Índice de Seguridad de la Información]].
