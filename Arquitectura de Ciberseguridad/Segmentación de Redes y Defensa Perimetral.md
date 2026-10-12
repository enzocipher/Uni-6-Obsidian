---
tags:
  - ciberseguridad
  - arquitectura
  - redes
  - segmentacion
  - dmz
  - sdn
materia: Arquitectura de Ciberseguridad
unidad: 2
sesion: 5
ciclo: 6to
---

# Sesión 5: Segmentación de Redes y Arquitectura de Defensa Perimetral

> *"La segmentación no es dividir por dividir: es contener el impacto donde el riesgo es mayor."*

## 1. Objetivo de la Sesión

* Diseñar segmentación por VLAN, zonas de confianza y DMZ aplicando gestión de riesgos y defensa en profundidad.
* Describir la microsegmentación con redes definidas por software (SDN).
* Comparar el perímetro clásico con arquitecturas distribuidas.
* Representar una arquitectura de red en Cisco Packet Tracer o Draw.io. En los ejercicios descritos, la herramienta se usa para diagramar; no se requiere configurar dispositivos.

La segmentación aplica los principios de diseño seguro de la [[Defensa en Profundidad y Zero Trust|Sesión 4]] y materializa zonas justificadas por activos y riesgos.

---

## 2. Segmentación, Zonas de Confianza y DMZ

### 2.1 Segmentación de redes

La segmentación divide una red plana en subredes lógicas agrupadas por función, sensibilidad o nivel de confianza. El tráfico entre segmentos debe pasar por un punto de control, como un firewall o una ACL de un switch de capa 3.

Una **zona de confianza** agrupa activos con niveles de riesgo aceptable y reglas de acceso similares. Cuanto más sensible es la zona, más estrictas deben ser sus reglas de entrada y salida.

### 2.2 DMZ y arquitectura multicapa

La zona desmilitarizada (DMZ) aloja servicios que deben ser accesibles desde Internet, como portales, APIs o correo, sin exponer directamente la red interna. Puede quedar entre dos firewalls o detrás de un firewall de tres interfaces.

* **Permitido:** Internet a DMZ, solo por los puertos del servicio publicado; DMZ a red interna, únicamente para consultas específicas necesarias.
* **Restringido:** acceso desde la red interna a Internet sin pasar por proxy o firewall.
* **Prohibido por diseño:** conexión directa de Internet a la red interna y acceso irrestricto de la DMZ a la red interna.

La idea clave es que cada transición entre capas atraviese un punto de control; ningún flujo debe saltar directamente de Internet a la red interna.

### 2.3 Ejemplo de zonas

| Segmento | Contenido | Tratamiento |
| :--- | :--- | :--- |
| VLAN 10 | Administración | Alta confianza, acceso controlado |
| VLAN 20 | Operaciones o planta | Confianza media; considerar riesgo operativo |
| VLAN 30 | Servidores internos | Alta sensibilidad y acceso estricto |
| VLAN 40 | Videovigilancia e IoT | Baja confianza, tráfico aislado |
| VLAN 99 | Invitados y Wi-Fi público | Sin confianza; salida a Internet únicamente |
| DMZ | Portal o API pública | Expuesta a Internet y aislada de VLAN internas |

---

## 3. SDN y Microsegmentación

### 3.1 Redes definidas por software

SDN separa el **plano de control**, que toma decisiones de enrutamiento y política, del **plano de datos**, que reenvía paquetes. Un controlador programa reglas de manera centralizada en los switches.

Esto facilita crear y cambiar políticas de segmentación sin configurar cada switch por separado y proporciona una base técnica para la microsegmentación.

### 3.2 Microsegmentación

La microsegmentación asigna un microperímetro de políticas a cada carga de trabajo (servidor, máquina virtual o contenedor), en vez de confiar en que todos los equipos dentro de una VLAN grande sean equivalentes.

| Enfoque | Frontera | Riesgo si un equipo se compromete |
| :--- | :--- | :--- |
| VLAN | Un perímetro alrededor del segmento | Puede haber movimiento lateral dentro de la VLAN |
| Microsegmentación | Política individual por carga de trabajo | Las reglas individuales limitan el movimiento lateral |

### 3.3 Evolución del perímetro

| Criterio | Perimetral clásico | Arquitectura distribuida |
| :--- | :--- | :--- |
| Frontera de confianza | Un perímetro en el borde | Microperímetros por activo o carga |
| Ubicación de activos | Datacenter centralizado | On-premises, nube, remoto y SaaS |
| Supuesto | Lo interno es confiable | Ninguna conexión es confiable por defecto |
| Control | Firewall perimetral | Políticas por identidad y segmento |
| Riesgo principal | Movimiento lateral tras vulnerar el borde | Gestión de identidades y políticas distribuidas |

La segmentación y la DMZ trazan fronteras; SDN puede acercar la frontera a cada carga de trabajo; las arquitecturas distribuidas asumen que ya no existe un único perímetro.

---

## 4. Caso Guiado: Grupo Minero Altas Cumbres

### 4.1 Contexto y activos

La empresa minera digitalizó operaciones y servicios sin dejar de operar una red plana. Sus activos y zonas incluyen:

* Administración: finanzas, RR. HH. y gerencia; planillas y contratos.
* Operaciones SCADA: monitoreo y control de la planta de procesamiento.
* Videovigilancia e IoT: cámaras y sensores de perímetro.
* Portal de proveedores: servicio web para facturas y seguimiento de pagos.
* Servidores internos: ERP, base de datos de producción y archivos.
* Wi-Fi de visitantes: auditores, contratistas y visitas.

### 4.2 De requisitos a zonas

Los requisitos lógicos del caso son separar SCADA de la oficina, tratar el portal como servicio público y aplicar controles estrictos a administración y servidores internos. La valoración de riesgos establece estas prioridades:

| Activo o zona | Amenaza principal | Nivel | Zona resultante |
| :--- | :--- | :--- | :--- |
| SCADA / Operaciones | Sabotaje o error que detenga la planta | Alto | Zona crítica, aislada |
| Portal de proveedores | Ataque desde Internet | Alto | DMZ |
| ERP / servidores internos | Acceso no autorizado a datos de producción | Alto | Zona sensible |
| Administración | Fuga de planillas o contratos | Medio | Zona controlada |
| Videovigilancia / IoT | Firmware desactualizado | Medio | Zona aislada de IoT |
| Wi-Fi de visitantes | Uso malicioso de un equipo externo | Bajo a medio | Zona no confiable |

### 4.3 Esquema de segmentación resultante

| VLAN o zona | ID | Contenido |
| :--- | :--- | :--- |
| Administración | VLAN 10 | Equipos de gerencia, finanzas y RR. HH. |
| Operaciones (SCADA) | VLAN 20 | Estaciones de monitoreo y control |
| Servidores internos | VLAN 30 | ERP y base de datos de producción |
| Videovigilancia / IoT | VLAN 40 | Cámaras y sensores |
| Invitados / Wi-Fi | VLAN 99 | Auditores, contratistas y visitantes |
| DMZ | — | Servidor del portal de proveedores |

La zona SCADA no debe aceptar acceso directo desde administración o Internet. El portal permanece en la DMZ. Los servidores reciben solo flujos explícitamente autorizados, y la red de visitantes carece de rutas a las demás VLAN.

### 4.4 Alternativas perimetrales

**Firewall de tres interfaces:** un único dispositivo controla Internet, DMZ y LAN. Reduce costo y concentra la administración, pero crea un punto único de falla.

**Doble firewall con IPS en línea (*screened subnet*):** dos firewalls separan Internet, DMZ y LAN; un IPS inspecciona el tráfico antes de llegar al servidor público. Un firewall externo comprometido no da acceso directo a la LAN. La solución aumenta el costo y la complejidad operativa.

---

## 5. Caso Grupal: NeoFin Digital

El caso plantea un banco digital con oficina principal en Lima, sucursal en Arequipa y una API de préstamos consumida por socios fintech. El riesgo principal es el acceso indebido a la API o a las cuentas de transacciones.

El ejercicio de clase pide representar dos sedes conectadas por WAN, separar al menos operaciones/atención al cliente y administración/TI, colocar la API en una DMZ accesible desde Internet y mantener el core bancario en una VLAN de servidores sin acceso directo desde la DMZ o la sucursal. Cada frontera debe justificarse mediante los activos, riesgos y principios de Zero Trust estudiados en sesiones anteriores.

---

## 6. Conclusiones Clave

1. Cada VLAN y DMZ debe responder a un activo y un riesgo identificados.
2. La DMZ publica servicios sin convertirlos en parte de la red interna.
3. SDN facilita la gestión centralizada de políticas; la microsegmentación limita movimiento lateral por carga de trabajo.
4. Packet Tracer y Draw.io permiten comunicar una decisión arquitectónica antes de implementarla.

## 7. Referencias

* NIST SP 800-207, *Zero Trust Architecture*.
* Cisco Systems, Cisco Packet Tracer.
* Open Networking Foundation, *SDN Architecture Overview*.
* Sherwood, Clark y Lynas, *Enterprise Security Architecture* (SABSA).
* ISO/IEC 27001:2022, *Information Security Management Systems — Requirements*.
