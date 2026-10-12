---
tags: [ciberseguridad, industrial, protocolos, iec62443]
materia: Ciberseguridad en Entornos Industriales y Cloud
unidad: 1
sesion: 3
ciclo: 6to
diapositivas: 59
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546143_1/file/_75805586_1?courseId=_546143_1
---

# Sesión 3: Protocolos industriales y requisitos de seguridad IEC 62443

## 1. Objetivo

Ubicar protocolos industriales en OSI, identificar sus riesgos estructurales, relacionarlos con IEC 62443 y explicar qué controles caben en los niveles 0, 1 y 2 de Purdue.

## 2. Marcos y roles

| Referencia | Uso en el curso |
|---|---|
| NIST CSF 2.0 | Gobierno del riesgo y comunicación con gerencia |
| NIST SP 800-82 Rev. 3 | Guía para aplicar seguridad en OT y adaptar controles |
| ISA/IEC 62443 | Requisitos verificables de programa, sistema y componente |

La familia 62443 se divide en **1-x** general, **2-x** políticas y procedimientos, **3-x** sistema y **4-x** componente. Siempre se cita la parte concreta.

| Rol | Responsabilidad y partes |
|---|---|
| Product supplier | Desarrollo seguro 4-1; requisitos del componente 4-2; declara capacidad SL-C |
| System integrator | Servicios 2-4; diseño de zonas y conduits 3-2; integración del sistema |
| Asset owner | Programa 2-1; define objetivos según riesgo; opera y mide el nivel alcanzado |

Comprar un controlador certificado y conectarlo sin separación al ERP no garantiza la seguridad de la instalación. La configuración, integración y operación siguen siendo responsabilidades distintas.

## 3. Los siete requisitos fundamentales

| FR | Nombre | Pregunta |
|---|---|---|
| FR1, IAC | Identification and Authentication Control | ¿Quién o qué se conecta y cómo se comprueba? |
| FR2, UC | Use Control | ¿Qué acciones puede realizar? |
| FR3, SI | System Integrity | ¿Se alteraron lógica, firmware o datos? |
| FR4, DC | Data Confidentiality | ¿Se puede leer información sensible? |
| FR5, RDF | Restricted Data Flow | ¿Qué zonas y comunicaciones están permitidas? |
| FR6, TRE | Timely Response to Events | ¿Se registra, detecta y responde a tiempo? |
| FR7, RA | Resource Availability | ¿Resiste sobrecarga, DoS y fallas? |

Cada FR se despliega en requisitos del sistema **SR** y mejoras **RE**. Los requisitos de componente son **CR**.

## 4. Security Levels

| Nivel | Perfil de amenaza descrito en la sesión |
|---|---|
| SL0 | Sin requisitos definidos |
| SL1 | Violación casual o accidental |
| SL2 | Ataque intencional con medios simples, recursos bajos y conocimiento genérico |
| SL3 | Medios sofisticados, recursos moderados y habilidades específicas IACS |
| SL4 | Medios sofisticados, recursos extendidos y alta motivación |

El SL se define por zona y riesgo; no es una nota de madurez ni el precio de un firewall.

- **SL-T, Target:** objetivo de diseño.
- **SL-C, Capability:** capacidad declarada del producto o sistema bajo las condiciones correspondientes.
- **SL-A, Achieved:** nivel realmente alcanzado en la instalación.

SL-A < SL-C orienta a configuración y operación; SL-C < SL-T requiere revisar capacidad y controles compensatorios; la distancia entre objetivo y realidad se convierte en un plan de trabajo.

## 5. Por qué faltaba seguridad en los protocolos

Los protocolos clásicos nacieron con aislamiento físico, recursos mínimos, prioridad de determinismo e interoperabilidad. Al transportarlos sobre Ethernet/IP se amplió su alcance sin incorporar automáticamente autenticación o cifrado.

El material utiliza OSI de forma didáctica. La ausencia de capas explícitas 5–6 no demuestra por sí sola que sea imposible autenticar: lo relevante es qué funciones incorpora cada protocolo y su configuración.

| Protocolo | Transporte o identificador | Seguridad descrita | Uso típico |
|---|---|---|---|
| Modbus RTU | Serie RS-485 | Sin autenticación ni cifrado nativos | Campo/control |
| Modbus TCP | TCP 502 | Sin autenticación ni cifrado en versión clásica | PLC–HMI |
| DNP3 | TCP 20000 o serie | Secure Authentication opcional; TLS aparte | Utilities y RTU |
| PROFINET RT | Capa 2, EtherType 0x8892 | Sin seguridad en el modo clásico presentado | Campo/control |
| EtherNet/IP + CIP | TCP 44818, UDP 2222 | CIP Security opcional | Control/supervisión |
| S7comm | TCP 102 | Protocolo propietario legado, protección limitada | Ingeniería/control |
| OPC UA | TCP 4840 | Identidad, firma y cifrado configurables | Supervisión e intercambio |

### Modbus RTU y TCP

La PDU conserva **function code + datos**. En serie se usan dirección del esclavo y CRC-16; TCP añade direccionamiento IP y cabecera MBAP y permite varios clientes. El CRC de la trama serie no se conserva en Modbus TCP.

MBAP tiene 7 bytes: Transaction ID 2, Protocol ID 2, Length 2 y Unit ID 1. Le siguen function code y datos. Estos campos no identifican al usuario ni impiden por sí mismos la repetición de un comando.

| FC | Operación | Riesgo |
|---|---|---|
| 01/02 | Leer coils/entradas digitales | Reconocimiento |
| 03/04 | Leer holding/input registers | Estado y consignas expuestos |
| 05 | Escribir una coil | Accionar motor o válvula |
| 06 | Escribir registro | Cambiar setpoint |
| 15/16 | Escribir múltiples coils/registros | Cambio de bloque |
| 08, subfunción 04 | Listen Only | Interrupción de respuestas |
| 43/14 | Identificación del dispositivo | Fabricante, modelo y firmware |

Un firewall industrial puede distinguir lectura y escritura dentro del mismo TCP 502. La variante Modbus/TCP Security introduce TLS en el puerto 802 según la presentación.

### DNP3

Incluye report by exception, marcas de tiempo en origen, respuestas no solicitadas y Select Before Operate. Es útil para largas distancias y enlaces limitados. Sobre TCP conserva su estructura interna: un filtro IP no interpreta automáticamente sus direcciones y comandos lógicos.

Funciones relevantes: Read/Write 1/2; Select/Operate 3/4; Direct Operate 5/6; Cold/Warm Restart 13/14; Disable Unsolicited Responses 21.

Secure Authentication usa desafío/respuesta y HMAC para autenticación e integridad, pero no cifra el contenido. TLS aporta confidencialidad aparte. Su despliegue enfrenta gestión de claves, equipos legacy, ventanas de parada y requisitos de compra. Una capacidad disponible puede estar desactivada.

### OPC UA

Se auditan tres decisiones independientes:

1. MessageSecurityMode: None, Sign o SignAndEncrypt.
2. SecurityPolicy: algoritmo y política habilitados.
3. UserTokenType: Anonymous, UserName o Certificate.

El material menciona Basic256Sha256, Aes128_Sha256_RsaOaep y Aes256_Sha256_RsaPss; señala Basic128Rsa15 y Basic256 como políticas antiguas. Un servidor en None y Anonymous conserva una superficie insegura aunque OPC UA admita controles sólidos.

## 6. Riesgos y correspondencia con controles

| Debilidad | Referencia de la presentación | Control |
|---|---|---|
| Sin autenticación | FR1, SR1.2 | Identidad del emisor o control compensatorio del conduit |
| Sin cifrado | FR4, SR4.1 | Canal seguro donde sea viable |
| Comando fuera de rango | FR3, SR3.5 | Validación e interlocks en lógica |
| Sin registro de acción | FR6, SR6.2 | Monitoreo y registro externo |

El mini caso de dosificación de agua sigue: descubrir TCP 502 → leer registros → identificar la consigna → enviar FC06 con valor excesivo → el PLC ejecuta → falta atribución del cambio. El caso de Oldsmar se presenta con la salvedad de que reportes posteriores cuestionaron la interpretación inicial de intrusión.

ATT&CK for ICS aporta táctica, técnica e ID: T0846 descubrimiento, T0842 captura, T0861 identificación de puntos, T0855 comando no autorizado, T0836 cambio de parámetro, T0814 DoS y T0831 manipulación del control. Estos mapeos son los del material docente, no una auditoría independiente del catálogo.

## 7. Controles por nivel

| Nivel 0 | Nivel 1 | Nivel 2 |
|---|---|---|
| Gabinetes y precintos | Selector RUN y alarma de cambio | Identidades nominales y RBAC |
| Redundancia de medición | Servicios mínimos | MFA para ingeniería según tarea |
| Protección de escritura HART | Validación de rango e interlocks | Aplicaciones permitidas |
| SIS independiente | Maestros y function codes permitidos | Control de USB |
| Inventario TAG/rango/calibración | Integridad de lógica | Parches probados en ventana |
| Custodia del calibrador | Backup offline probado | Logs centralizados y hora sincronizada |

Las recomendaciones de MFA deben evaluarse con la operación: la presentación distingue ingeniería privilegiada de maniobras urgentes en HMI. No es una prohibición general de autenticar al operador.

## 8. Laboratorio del material

Topología de estudio en VPC 10.128.0.0/24: OpenPLC en .2, ScadaBR en .3 y estación de análisis en .4. La captura se hace en el endpoint .3; una VPC de capa 3 no permite asumir que un tercer servidor observa todo el tráfico.

Fases: descubrir puertos → capturar → mapear registros → demostrar escritura en la simulación → buscar evidencia → aplicar controles y repetir.

```bash
# Ejemplos transcritos del laboratorio docente, sobre sus máquinas simuladas
nmap -Pn -sT -p 102,502,4840,20000,44818 10.128.0.0/24
nmap -Pn -p 502 --script modbus-discover 10.128.0.2
sudo tshark -i ens4 -f "tcp port 502" -w modbus_base.pcap
mbpoll -m tcp -a 1 -r 1 -c 16 -t 4 -1 10.128.0.2
mbpoll -m tcp -a 1 -r 1 -t 0 10.128.0.2 1
mbpoll -m tcp -a 1 -r 4 -t 4 10.128.0.2 9999
tshark -r modbus_base.pcap -Y "mbtcp.modbus.func_code >= 5"
iptables -A INPUT -p tcp --dport 502 ! -s 10.128.0.3 -j DROP
```

El filtro por origen restringe alcance; la validación en ST neutraliza entradas inválidas; la captura documenta la acción. Son tres controles distintos. Las estimaciones SL antes/después de los ejercicios son simplificaciones pedagógicas y no certifican una zona.

## 9. Actividades, conclusiones y referencias

- Marcar enlaces en claro entre IT, IDMZ, SCADA, PLC y campo; OPC UA depende del modo configurado.
- Distinguir cifrado de segmentación: una VPN directa al PLC puede cifrar y, aun así, saltar la frontera.
- No aplicar el criterio de cifrado de paquetes a una señal analógica 4–20 mA.
- Debatir latencia, jitter, capacidad del hardware y parque instalado.
- Exponer un control con amenaza/ATT&CK, FR/SR, nivel/zona, efecto operacional y SL-T justificado.

Referencias: MITRE ATT&CK for ICS; CISA Recommended Practices; IEC 62443-3-3, 3-2 y 4-2; NIST SP 800-82 Rev. 3; IEEE 1815; Modbus Application Protocol Specification.

Anterior: [[Arquitectura ICS y modelo de Purdue]]. Siguiente: [[Amenazas industriales, casos históricos y modelado de amenazas]]. Volver: [[Índice de Ciberseguridad en Entornos Industriales y Cloud]].
