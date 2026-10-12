---
tags:
  - ciberseguridad
  - arquitectura
  - zero_trust
  - ztna
  - sase
  - acceso_remoto
materia: Arquitectura de Ciberseguridad
unidad: 2
sesion: 6
ciclo: 6to
---

# Sesión 6: Zero Trust Network Access (ZTNA) y SASE

> *"La VPN te deja entrar a la red. ZTNA solo te deja llegar a la aplicación que necesitas."*

## 1. Objetivo de la Sesión

* Diseñar acceso Zero Trust con ZTNA e identificar PE, PA y PEP según NIST SP 800-207.
* Explicar SASE como convergencia de red (SD-WAN) y seguridad (SSE) en la nube.
* Comparar ZTNA y VPN tradicional y plantear una migración gradual.
* Diagramar una arquitectura de acceso para un caso organizacional.

ZTNA lleva a la práctica el modelo de [[Defensa en Profundidad y Zero Trust|Zero Trust de la Sesión 4]] y complementa las fronteras de red y zonas desarrolladas en la [[Segmentación de Redes y Defensa Perimetral|Sesión 5]].

---

## 2. Del Acceso por Red al Acceso por Aplicación

### 2.1 Límites de la VPN tradicional

La VPN suele conectar al usuario remoto a un segmento de red. Una vez autenticado, puede existir confianza implícita dentro del túnel y la sesión no siempre vuelve a evaluar dispositivo o contexto.

1. Se concede acceso a una red, no necesariamente a una sola aplicación.
2. Una credencial comprometida puede facilitar movimiento lateral.
3. El concentrador VPN está expuesto a Internet.
4. El tráfico puede regresar al datacenter para ser inspeccionado, incluso cuando su destino está en la nube (backhaul).

### 2.2 Qué es ZTNA

Zero Trust Network Access aplica los principios de Zero Trust al acceso. Un intermediario verifica identidad, dispositivo y contexto en cada solicitud y establece una conexión individual únicamente con la aplicación autorizada. Las demás aplicaciones permanecen invisibles para ese usuario.

* **Acceso por aplicación:** se crea una sesión hacia un recurso concreto, no acceso general a una IP o red.
* **Aplicaciones invisibles:** los puertos de las aplicaciones no se publican directamente; sin autorización previa no se descubren.
* **Verificación continua:** la decisión puede reevaluarse si cambia el riesgo del usuario o del dispositivo.

### 2.3 Componentes de una arquitectura ZTNA

| Componente | Función |
| :--- | :--- |
| Policy Engine (PE) | Decide permitir, denegar o revocar el acceso con base en la política y señales de riesgo |
| Policy Administrator (PA) | Ejecuta la decisión, establece o cierra el canal y gestiona credenciales o tokens de sesión |
| Policy Decision Point (PDP) | Agrupa PE y PA: toma y coordina la decisión de acceso |
| Policy Enforcement Point (PEP) | Habilita, monitorea y termina la conexión entre sujeto y recurso |
| Fuentes de información | IdP/IAM y MFA, MDM/EDR, inteligencia de amenazas, SIEM, PKI, políticas de datos y cumplimiento |

El sujeto solicita acceso al PEP. El PDP consulta las fuentes de contexto y decide. Si se permite, el PA configura una sesión limitada y el PEP hace cumplir la política. Si no existe una autorización explícita, el PEP deniega el acceso.

### 2.4 Modelos de despliegue

| Modelo | Uso habitual | Ventajas y límites |
| :--- | :--- | :--- |
| Iniciado por cliente (con agente) | Personal con equipos corporativos | Evalúa postura en tiempo real y admite protocolos como RDP o SSH; requiere equipos gestionados |
| Iniciado por servicio (portal sin agente) | Terceros, contratistas y BYOD | Útil para aplicaciones web y equipos no gestionados; el conector puede iniciar una conexión saliente hacia el broker |

Una organización puede combinar ambos: agente para dispositivos corporativos y portal para terceros con permisos más acotados.

---

## 3. SASE y SSE

### 3.1 Concepto

**SASE (Secure Access Service Edge)** integra funciones de red de área amplia (SD-WAN) y seguridad (SSE) como un servicio en la nube. La política se aplica en un punto de presencia (PoP) próximo al usuario o sede.

**SASE = SD-WAN + SSE**

**SSE = ZTNA + SWG + CASB + FWaaS**

Zero Trust es una estrategia o principio; ZTNA es una tecnología para aplicar ese principio al acceso a aplicaciones privadas; SASE es un modelo de entrega que integra ZTNA con red y otras funciones de seguridad. DLP puede complementar las capacidades de seguridad de la plataforma.

### 3.2 Bloques funcionales

| Componente | Función |
| :--- | :--- |
| SD-WAN | Conecta sedes, nubes y datacenter eligiendo rutas como Internet, MPLS o 4G/5G; reduce el backhaul |
| ZTNA | Controla el acceso por identidad y contexto a aplicaciones privadas |
| SWG | Filtra navegación web y bloquea amenazas o sitios no permitidos |
| CASB | Da visibilidad y control sobre el uso de aplicaciones SaaS |
| FWaaS | Entrega funciones de firewall como servicio |
| DLP | Inspecciona datos sensibles para reducir su fuga |
| Gestión unificada | Centraliza políticas y registros para alimentar SIEM/SOC |

La evaluación arquitectónica debe revisar cobertura e integración de políticas y registros, no solo la marca del proveedor.

### 3.3 Hub-and-spoke y borde SASE

En un modelo *hub-and-spoke*, el tráfico de sucursales y usuarios remotos puede viajar primero al datacenter para alcanzar Internet o SaaS. En SASE, los usuarios y sedes se conectan al PoP adecuado, reciben inspección en el borde y siguen hacia su destino. La decisión de política acompaña el acceso aunque aplicaciones y usuarios estén distribuidos.

---

## 4. VPN frente a ZTNA y Ruta de Migración

| Criterio | VPN tradicional | ZTNA |
| :--- | :--- | :--- |
| Unidad de acceso | Red o segmento | Aplicación individual |
| Confianza | Implícita tras autenticarse | Explícita y reevaluada por solicitud |
| Señales | Credenciales y, a veces, MFA | Identidad, MFA, postura y contexto |
| Visibilidad | Recursos descubribles dentro del túnel | Aplicaciones invisibles sin autorización |
| Movimiento lateral | Posible dentro de la red alcanzada | Limitado al recurso autorizado |
| Terceros y BYOD | Puede requerir entregar acceso de red | Portal sin agente con permisos restringidos |
| Nube | Puede forzar backhaul al datacenter | Integración nativa con servicios en la nube |

La VPN puede mantenerse temporalmente para administración de red o sistemas heredados, con excepciones documentadas, mientras se completa la migración.

### Hoja de ruta

1. **Inventariar:** usuarios, dispositivos, aplicaciones, flujos y criticidad.
2. **Fortalecer identidad:** IdP central, MFA y gestión de dispositivos con MDM/EDR.
3. **Pilotear ZTNA:** publicar una o dos aplicaciones críticas para un grupo reducido, por ejemplo terceros.
4. **Migrar y retirar VPN:** mover el resto de aplicaciones y conservar solo excepciones justificadas.
5. **Converger en SASE:** sumar SD-WAN, SWG y CASB bajo una política integrada.

Como referencia de madurez, el Zero Trust Maturity Model de CISA v2.0 contempla cinco pilares (identidad, dispositivos, redes, aplicaciones y datos) y niveles de tradicional, inicial, avanzado y óptimo.

---

## 5. Caso Guiado: Agroexportadora Valle Verde

### 5.1 Situación y riesgo

Valle Verde exporta uva y palta. Tiene sede administrativa y datacenter en Lima, planta de empaque y cámaras de frío en Ica, ERP propio, aplicación de trazabilidad en IaaS, Microsoft 365 y un portal para operadores logísticos.

Un operador logístico entregó sus credenciales VPN tras un phishing. El atacante se conectó a la red plana, alcanzó archivos y la base de datos de exportaciones, y detuvo despachos durante dos días. El objetivo directivo es impedir que un tercero pueda ver toda la red.

| Recurso | Ubicación | Usuario que necesita acceso | Riesgo con VPN | Nivel |
| :--- | :--- | :--- | :--- | :--- |
| ERP (finanzas y ventas) | Datacenter Lima | Analistas | Cualquier usuario VPN alcanza el ERP | Alto |
| Portal de exportaciones | DMZ Lima | Operadores externos | Robo de credenciales de terceros | Alto |
| Control de cámaras de frío (OT) | Planta Ica | Operarios y proveedor de mantenimiento | Manipulación remota y pérdida de carga | Alto |
| Base de datos de exportaciones | Datacenter Lima | ERP y TI | Movimiento lateral desde la VPN | Alto |
| App de trazabilidad | Nube IaaS | Técnicos de campo | Tabletas sin postura controlada | Medio |
| Microsoft 365 | SaaS | Colaboradores | Tráfico no inspeccionado fuera de Lima | Medio |

### 5.2 Matriz de políticas

| Sujeto | Recurso | Condiciones | Decisión |
| :--- | :--- | :--- | :--- |
| Analista de finanzas | ERP, solo módulo de finanzas | MFA y laptop corporativa con EDR activo | Permitir con agente |
| Operador logístico externo | Portal, solo sus embarques | MFA, sesión web de hasta 8 horas, limitar descargas masivas | Permitir por portal |
| Proveedor de mantenimiento OT | Control de cámaras de frío | MFA, aprobación previa, ventana de 2 horas y sesión grabada | Permitir temporalmente, just-in-time |
| Técnico de campo | App de trazabilidad | Tableta gestionada por MDM y ubicación en Perú | Permitir |
| Cualquier sujeto | Recurso no listado | No existe política que autorice el acceso | Denegar |

### 5.3 Arquitectura propuesta y alternativas

La arquitectura propuesta usa una nube SASE con PoP en Lima, PEP ZTNA, PDP (PE y PA), IdP/MFA, MDM/EDR y SIEM. El personal accede con agente; los operadores externos usan un portal. Un conector en el datacenter llega a la VLAN del ERP/base de datos y a la DMZ del portal. La planta de Ica se conecta mediante SD-WAN a la VLAN OT. SWG, CASB, FWaaS y DLP protegen el acceso a Internet y SaaS. La VPN se retira al completar la migración; las VLAN de la [[Segmentación de Redes y Defensa Perimetral|Sesión 5]] se mantienen como segunda capa.

| Alternativa | Ventajas | Límites |
| :--- | :--- | :--- |
| ZTNA autogestionado en el datacenter, sin SASE | Control local de PE, PA, PEP y registros; evita costo por usuario de un servicio SASE | Gateway publicado en Internet; Ica y SaaS mantienen backhaul; TI opera alta disponibilidad, capacidad y parches |
| Transición híbrida: ZTNA primero para terceros | Atiende rápidamente el vector del incidente y tiene menor costo inicial | Conviven VPN y ZTNA, consolas y registros; empleados conservan confianza implícita en su VLAN |

### 5.4 Representación en Packet Tracer o Draw.io

El ejercicio propone diagramar los componentes lógicos con dispositivos rotulados; las herramientas no simulan ZTNA o SASE ni requieren configurar direcciones IP, políticas o túneles.

| Componente lógico | Representación sugerida |
| :--- | :--- |
| Nube SASE / Internet | Cloud-PT rotulada como PoP SASE |
| PEP ZTNA | ASA rotulado como PEP ZTNA |
| PDP (PE + PA) | Servidor rotulado como PDP |
| IdP + MFA, MDM y SIEM | Servidores rotulados por fuente |
| Conector ZTNA en Lima | Servidor junto al switch del datacenter |
| SD-WAN Edge en Ica | Router rotulado SD-WAN Edge |
| Usuarios y recursos | Equipos de usuario y servidores colocados en las VLAN/zonas correspondientes |

El diagrama debe mostrar los perfiles de usuario, el PEP, el plano de control, las fuentes de señal, Lima, Ica y las políticas de acceso por recurso.

---

## 6. Propuesta de Trabajo por Equipos

El material plantea cuatro posibles organizaciones: Cooperativa Andes Crédito, BioAnálisis Perú, Universidad Tecnológica del Pacífico y MercaNorte. Cada propuesta debe incluir:

1. Inventario de sujetos, dispositivos y recursos, con los riesgos asociados.
2. Matriz de políticas con al menos cinco filas y denegación por defecto.
3. Diagrama con PE, PA, PEP, fuentes de información, usuarios y segmentos de red.
4. Justificación de ZTNA con agente, sin agente o ambos; decisión sobre SASE y tratamiento de la VPN.

---

## 7. Conclusiones Clave

1. ZTNA decide el acceso por aplicación y separa la decisión (PE/PA) de su aplicación (PEP).
2. SASE integra SD-WAN y seguridad SSE en la nube, cerca de usuarios y sedes.
3. La migración desde VPN se realiza por fases, con excepciones controladas.
4. Activos y riesgos, los principios de Zero Trust y la segmentación deben alimentar cada política.

## 8. Referencias

* NIST SP 800-207 (2020), *Zero Trust Architecture*.
* NIST SP 1800-35, *Implementing a Zero Trust Architecture* (NCCoE).
* CISA (2023), *Zero Trust Maturity Model*, versión 2.0.
* Gartner (2019), *The Future of Network Security Is in the Cloud*.
* Gilman, E. y Barth, D. (2017), *Zero Trust Networks: Building Secure Systems in Untrusted Networks*. O'Reilly.
* Cisco Systems, Cisco Packet Tracer.
