---
tags: [arquitectura, firewalls, ids, ips, nac, iam, pam]
materia: Arquitectura de Ciberseguridad
unidad: 2
sesion: 7
sesion_hasta: 8
ciclo: 6to
diapositivas: 21
actualizado: 2026-10-11
fuente: https://aulavirtual.upc.edu.pe/ultra/courses/_546141_1/file/_76058838_1?courseId=_546141_1
---

# Sesiones 7 y 8: Firewalls, IDS/IPS, NAC e identidad y gestión de accesos

## 1. Objetivo

Diseñar controles de red y una arquitectura de identidad, ubicando cada control según el riesgo que reduce. Se integran con ZTNA y SASE de la sesión 6.

La fuente reúne las sesiones 7 y 8 en una sola presentación. La propiedad `sesion` señala su inicio y `sesion_hasta` su cierre.

## 2. Tipos de firewall

| Tipo | Qué observa | Aplicación |
|---|---|---|
| Filtro de paquetes | IP, puerto y protocolo, capas 3 y 4 | Reglas de comunicación de red |
| Stateful | Paquetes y estado de las conexiones | Distinguir conexiones y sus respuestas permitidas |
| NGFW | Aplicación, usuario y funciones de inspección hasta capa 7 | Control de la frontera y amenazas según sus capacidades |
| WAF | Solicitudes web de capa 7 | Proteger aplicaciones publicadas frente a ataques web, como inyección SQL |

Los controles pueden complementarse. Un NGFW en la frontera y un WAF delante del portal cumplen funciones distintas.

## 3. Ubicación y dirección del tráfico

| Control | Ubicación propuesta | Riesgo que reduce |
|---|---|---|
| NGFW perimetral en alta disponibilidad | Frontera con Internet | Entradas y salidas no autorizadas |
| WAF | Delante del portal web en la DMZ | Ataques contra solicitudes y funciones web |
| Firewall interno, ISFW | Entre segmentos de usuarios y datacenter | Acceso directo y movimiento entre zonas |

**Norte-sur:** tráfico que entra o sale de la organización. **Este-oeste:** tráfico entre segmentos o sistemas internos.

La segmentación debe expresar comunicaciones necesarias. Separar una VLAN sin controlar los flujos entre zonas deja incompleta la protección.

## 4. IDS e IPS

| Aspecto | IDS | IPS |
|---|---|---|
| Posición | Recibe copia del tráfico, fuera de línea | Está en línea con el tráfico |
| Acción | Detecta y alerta | Puede detectar y bloquear |
| Consideración | Necesita un proceso que atienda las alertas | El bloqueo puede afectar tráfico legítimo |

| Método | Cómo detecta | Consideración |
|---|---|---|
| Firmas | Compara con patrones conocidos | Depende de cobertura y actualización |
| Anomalías | Identifica desviaciones de lo normal | Puede aumentar falsas alarmas |
| Análisis de protocolo | Revisa uso y comportamiento del protocolo | Requiere interpretación adecuada del tráfico |

Un falso positivo es una alerta sin ataque. Un falso negativo es un ataque que no genera alerta. En entornos donde una interrupción puede producir daño físico o afectar atención clínica, el modo de respuesta requiere una evaluación particular.

## 5. Ubicación de sensores

| Sensor | Lugar | Justificación de la presentación |
|---|---|---|
| IPS en línea | Después del NGFW | Detener ataques que superen el control perimetral |
| NIDS con SPAN | DMZ | Vigilar servidores expuestos |
| NIDS con TAP | Red interna | Detectar movimiento entre sistemas |
| HIDS | Servidores críticos, como ERP y base de datos | Observar eventos dentro del servidor, incluso cuando el tráfico de red está cifrado |

Los sensores envían eventos al SIEM/SOC para correlación y atención. Tener visibilidad en un único punto deja fuera otras partes del recorrido.

## 6. NAC y 802.1X

NAC decide qué dispositivo obtiene conectividad y a qué segmento puede ingresar. El flujo docente es:

1. El equipo se conecta al switch o punto de acceso.
2. El puerto permite inicialmente el intercambio necesario para identificación.
3. NAC valida identidad y postura del equipo, por ejemplo parches y antivirus.
4. El switch aplica la VLAN o política correspondiente.

| Resultado | Segmento propuesto |
|---|---|
| Equipo corporativo conforme | VLAN corporativa |
| Equipo sin parches o protección requerida | Cuarentena |
| Visitante o equipo personal | Invitados, con salida a Internet |
| Impresora, cámara o sensor | IoT con comunicaciones restringidas |

Para equipos sin soporte de 802.1X, el material utiliza **MAB**, reconocimiento por dirección MAC, y una VLAN restringida. MAB no ofrece la misma prueba de identidad que un mecanismo criptográfico; su aplicación necesita controles compensatorios y segmentación.

## 7. Identidad: preguntas y ciclo de vida

| Función | Pregunta |
|---|---|
| Identificación | ¿Quién dices ser? |
| Autenticación | ¿Puedes demostrarlo? |
| Autorización | ¿Qué puedes hacer? |
| Auditoría | ¿Qué hiciste? |

El ciclo incluye alta con accesos por rol, cambio con retiro y asignación de permisos, y baja con revocación oportuna. La presentación propone cerrar las cuentas el mismo día de la salida.

ZTNA y NAC dependen de información de identidad. Una cuenta de un extrabajador que permanece activa puede conservar acceso aunque los controles tecnológicos estén operativos.

## 8. MFA, RBAC y ABAC

MFA combina factores de tipos diferentes:

- Conocimiento: contraseña o PIN.
- Posesión: celular o llave de seguridad.
- Característica personal: huella o rostro.

Dos contraseñas no constituyen MFA. La sesión compara contraseña sola, SMS, códigos o notificaciones de aplicación, y llaves físicas o passkeys. Destaca la resistencia al phishing de las últimas y propone MFA general con protección reforzada para administradores.

La lámina incluye una dirección de ordenamiento contradictoria con sus ejemplos. Se conserva la relación conceptual: una contraseña sola no es MFA; SMS y códigos pueden ser objeto de phishing; llaves o passkeys apropiadamente implementadas ofrecen mayor resistencia a ese ataque.

| Modelo | Cómo autoriza | Ejemplo |
|---|---|---|
| RBAC | Asigna permisos a roles y los hereda el usuario | Analista de finanzas accede al módulo de pagos |
| ABAC | Combina atributos de usuario, recurso y contexto | Acceso si pertenece a finanzas, usa equipo corporativo y está en horario autorizado |

Se aplican mínimo privilegio, separación de funciones y revisión periódica. Quien registra un proveedor no debería aprobar por sí solo su pago.

## 9. Identidad centralizada, federación y SSO

| Diseño | Relación de confianza | Uso ilustrativo |
|---|---|---|
| Centralizado | Un directorio e IdP para la organización | Personal y aplicaciones corporativas |
| Federado | Una organización confía en la identidad confirmada por otra | Socios, proveedores, médicos externos o SaaS |

En federación, la aplicación receptora confía en las afirmaciones del IdP de origen en lugar de almacenar la contraseña del usuario.

| Protocolo | Función destacada |
|---|---|
| SAML 2.0 | Identidad y SSO corporativo en aplicaciones web/SaaS |
| OAuth 2.0 | Delegación de acceso limitado a una aplicación |
| OpenID Connect | Identidad sobre OAuth 2.0, usado en web y móvil |

Flujo conceptual SSO: el usuario entra a una aplicación, esta lo dirige al IdP, el IdP autentica con MFA y entrega evidencia firmada que la aplicación valida. Las sesiones, tokens y permisos necesitan políticas de revocación para que una baja sea efectiva.

## 10. PAM y acceso privilegiado

El esquema docente coloca una plataforma PAM entre administrador o proveedor y servidores, bases de datos o dispositivos de red:

| Capacidad | Resultado |
|---|---|
| Bóveda de credenciales | Custodia y rotación de contraseñas administrativas |
| Acceso aprobado y temporal | Privilegios disponibles durante el trabajo autorizado |
| Sesión registrada | Evidencia para auditoría y monitoreo |
| Integración con SIEM | Correlación de actividad privilegiada |

La presentación propone ocultar las credenciales reales al usuario y cambiarlas después del uso. Estas funciones dependen de la solución y su integración; son objetivos del diseño mostrado.

## 11. Caso guiado: Agroexportadora Valle Verde

El acceso remoto ya utiliza ZTNA/SASE. La auditoría identifica cinco problemas internos en Lima e Ica.

| Hallazgo | Control propuesto |
|---|---|
| Portal de exportaciones recibe ataques web | WAF en DMZ, con NGFW perimetral |
| Usuarios llegan directamente a la base de datos | Firewall interno; la aplicación ERP media el acceso |
| Puertos y Wi-Fi admiten cualquier equipo | NAC, RADIUS y 802.1X con asignación de segmentos |
| Cámaras de frío OT sin monitoreo; bloqueo erróneo dañaría fruta | Firewall OT e IDS pasivo |
| Incidentes descubiertos por quejas | Registros de controles hacia SIEM |

### Topología y segmentos

En Lima: Internet/SASE, NGFW en alta disponibilidad, DMZ con WAF y portal, IPS en línea, núcleo y firewall interno hacia datacenter. Los accesos se distribuyen entre VLAN 10 usuarios, 30 datacenter, 40 invitados, 50 IoT y 99 cuarentena. ERP y base de datos requieren vigilancia; la base incorpora HIDS.

En Ica: conexión SD-WAN, firewall, switch de acceso, firewall OT y segmento de cámaras de frío con IDS pasivo. El acceso remoto continúa por el PEP ZTNA de la sesión 6.

### Matriz de reglas del ejemplo

| Origen | Destino | Acción | Justificación |
|---|---|---|---|
| Usuarios, VLAN 10 | ERP | Permitir | Función de trabajo |
| Usuarios, VLAN 10 | Base de datos | Denegar | Solo el ERP debe comunicarse con la BD |
| Invitados, VLAN 40 | Redes internas | Denegar | Su acceso se limita a Internet |
| Técnico OT mediante ZTNA | Cámaras de frío | Permitir durante 2 horas | Mantenimiento temporal y registrado |
| Cualquier origen | Cualquier destino restante | Denegar | Cerrar comunicaciones sin autorización explícita |

El ejemplo usa evaluación por primera coincidencia y deja la regla general al final. La regla explícita ERP hacia BD debe documentarse al completar la matriz técnica; las cinco filas mostradas son reglas clave del caso.

Laboratorio académico: partir de la topología de la sesión 6, añadir firewall interno y reglas, ubicar WAF/IPS/IDS/NAC/SIEM, crear VLANs y rotular qué hallazgo atiende cada control.

## 12. Caso grupal: Clínica Vida Plena

Escenario ficticio de una clínica de 120 camas, 600 colaboradores y datacenter propio. Contiene portal de citas/resultados, HIS, laboratorio, monitores y bombas de infusión, médicos externos con laptop, Wi-Fi de pacientes y visitantes, cajas y POS.

Incidente del caso: un médico externo conecta una laptop infectada; el ransomware recorre la red plana y cifra el servidor de laboratorio; los monitores de UCI pierden conexión con enfermería durante tres horas.

**Restricción:** los dispositivos biomédicos no admiten agentes ni 802.1X, y un bloqueo erróneo puede afectar la atención.

La actividad solicita:

1. Topología con firewalls, WAF, IDS/IPS, NAC, IdP y SIEM, ubicando activos por segmento.
2. Al menos seis reglas justificadas, con denegación general al final.
3. Política NAC para colaborador, médico externo, paciente, biomédico y POS.
4. Decisión de bloqueo o detección según el impacto sobre los equipos biomédicos.
5. MFA y SSO del personal, acceso de médicos externos y PAM de administradores o proveedor biomédico.

La consigna queda como ejercicio para el grupo, con exposición de tres minutos. La referencia legal de datos de salud se conserva como contexto del caso docente.

## 13. Repaso y referencias

1. ¿Qué diferencia hay entre NGFW, WAF y firewall interno?
2. ¿Qué tráfico observa cada sensor y qué queda fuera de su visibilidad?
3. ¿Qué riesgo introduce poner IPS en un flujo clínico crítico?
4. ¿Cómo se asigna acceso a un dispositivo sin 802.1X?
5. ¿Cómo se combinan IdP, NAC, ZTNA y PAM sin conservar accesos obsoletos?
6. ¿Qué reglas faltan para que la topología de Valle Verde sea implementable?

Referencias citadas por la presentación: NIST SP 800-41 Rev. 1, SP 800-94, IEEE 802.1X, OWASP Top 10 de 2021 y ModSecurity CRS, NIST SP 800-82 Rev. 3, SP 800-63B, SAML 2.0, RFC 6749 y OpenID Connect Core 1.0. Son las ediciones que el docente cita; esta nota no verifica su vigencia individual.

## Conexiones

- [[Segmentación de Redes y Defensa Perimetral]]
- [[ZTNA y SASE]]
- [[Identidades y Dispositivos en Zero Trust]]
- [[Autenticación, autorización y gestión de identidades en APIs]]
- [[Segmentación industrial, zonas, conduits y seguridad funcional]]
- [[Índice de Arquitectura de Ciberseguridad]]

## Fuente

**Sesiones7y8_FW_IDS_IPS_NAC_IAM_va**, presentación PDF revisada en el aula virtual el 11 de octubre de 2026. Se conservan conceptos, ubicación de controles, reglas y casos. Las aclaraciones sobre MFA, MAB, sesiones y reglas distinguen la simplificación docente de una configuración técnica completa.
