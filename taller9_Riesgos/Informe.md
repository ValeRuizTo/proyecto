# Análisis de Riesgos Arquitectónicos — Almacén Súper Amortiguadores LTDA

El presente documento constituye el Análisis de Riesgos para el proyecto de la empresa Almacén Súper Amortiguadores LTDA.

El objetivo central de este análisis es identificar, categorizar y priorizar los riesgos presentes en la arquitectura actual (AS-IS) de la organización, con el fin de fundamentar las decisiones arquitectónicas de la propuesta futura (TO-BE).

---

## 1. Contexto de la empresa

### 1.1 Descripción general

Almacén Súper Amortiguadores LTDA es una empresa del sector automotriz dedicada a la comercialización de repuestos y a la prestación de servicios de diagnóstico y reparación de vehículos. Opera desde un único punto físico con un equipo de aproximadamente siete (7) empleados.

### 1.2 Estado actual de la gestión de información (AS-IS)

La gestión de la información en la empresa se realiza de manera predominantemente manual, apoyada en herramientas básicas. Los elementos más relevantes del estado actual son:

- Existe un único documento en Google Docs denominado "facturas", que concentra el registro de ventas y algunos detalles de servicios.
- No existe un sistema estructurado para el control de inventario; la gestión depende de revisión visual de la bodega.
- No hay un sistema de gestión de citas; la programación de servicios se realiza por canales informales (WhatsApp, llamadas telefónicas).
- No existe un registro histórico de los vehículos atendidos ni de los servicios prestados.
- La información comercial y operativa está centralizada en un único documento, lo que representa un riesgo crítico de pérdida, corrupción o acceso no autorizado.

---

## 2. Relación AS-IS / TO-BE y Gap Analysis

El análisis de brechas permite identificar la distancia entre el estado actual y el estado futuro deseado, revelando los riesgos y necesidades de transformación.

| Arquitectura AS-IS | Arquitectura TO-BE | Brecha / Riesgo |
|---|---|---|
| Google Docs como único repositorio de información | Sistema de información centralizado con base de datos relacional (Cloud SQL / PostgreSQL) y modelo E-R formal | Crítico — Datos / Seguridad |
| Sin control de inventario digital | Módulo de inventario con trazabilidad de repuestos, alertas automáticas de stock mínimo y soporte para órdenes de compra | Crítico — Procesos / Negocio |
| Gestión de citas informal (WhatsApp/llamadas) | Módulo de solicitudes con estados (pendiente → en proceso → finalizado) y asignación del responsable por servicio | Alto — Procesos |
| Sin historial de vehículos ni servicios | Historial estructurado de clientes, vehículos y servicios en BD relacional, consultable por mecánicos en tiempo real | Crítico — Datos / Procesos |
| Sin control de acceso ni permisos por rol | Autenticación con OAuth 2.0 via IAP + autorización basada en roles para recepcionista, mecánico y administrador | Alto — Seguridad |
| Sin métricas ni observabilidad del negocio | Cloud Logging para auditoría completa de actividad + base para dashboard de indicadores de ventas e inventario | Moderado — Infraestructura |

---

## 3. Cuadrante de identificación de riesgos

| Análisis de Arquitectura (Sistema) | Análisis de Dependencias (Red) |
|---|---|
| El análisis de la arquitectura AS-IS revela ausencia de sistemas estructurados, dependencia de herramientas genéricas (Google Docs) y puntos únicos de falla en datos, procesos e infraestructura. | La dependencia de un único documento compartido implica que cualquier fallo (borrado accidental, pérdida de acceso, corrupción) afecta simultáneamente ventas, inventario y trazabilidad. |
| **Listas de Verificación (Histórico)** | **Consulta a Interesados (Personas)** |
| Se aplicaron los dominios de análisis de riesgo definidos en la guía metodológica: Negocio, Procesos, Datos, Aplicaciones, Infraestructura, Seguridad y Gobierno TI. | El levantamiento de información con los empleados y el dueño del negocio permitió identificar problemas operacionales reales: ausencia de trazabilidad, pérdida de información y desorganización en la atención. |

---

## 4. Análisis de riesgos por dominio AS-IS

A continuación se presenta el análisis detallado de los riesgos identificados en cada dominio de la Arquitectura Empresarial.

### 4.1 Riesgos de negocio

El negocio opera sin una plataforma tecnológica que soporte sus procesos críticos, lo que genera una brecha entre la capacidad de atención y el potencial de crecimiento.

- **Dependencia de conocimiento humano:** la gestión del inventario y las ventas depende de la memoria y criterio visual de empleados específicos.
- **Baja capacidad de adaptación:** sin datos históricos, es imposible tomar decisiones estratégicas como identificar repuestos de mayor rotación o temporadas de mayor demanda.
- **Experiencia del cliente comprometida:** la desorganización en la gestión de citas genera tiempos de espera innecesarios y percepción de baja profesionalización.
- **Procesos no documentados:** la falta de un historial hace que si los usuarios necesitan hacer alguna reclamación, sea imposible comprobar el servicio que se les prestó.

### 4.2 Riesgos de procesos

Los procesos operativos presentan vulnerabilidades críticas derivadas de la ausencia de automatización y digitalización:

- El proceso de registro de ventas es completamente manual, propenso a errores, duplicidades y omisiones.
- El proceso de inventario se basa en inspección visual de la bodega, sin registro de entradas ni salidas, generando pérdidas no detectadas y rupturas de stock.
- El agendamiento de servicios por WhatsApp no genera trazabilidad ni permite priorización, resultando en conflictos de agenda y clientes desatendidos.
- No existe formalización BPMN de los procesos actuales, lo que impide identificar cuellos de botella ni estandarizar la operación.

### 4.3 Riesgos de datos

La arquitectura de datos actual es el dominio con mayor concentración de riesgos:

- Un único archivo de Google Docs centraliza ventas, servicios y alguna información de clientes, sin estructura relacional, sin tipos de dato definidos y sin validaciones.
- No existe separación entre datos operacionales (ventas del día) e históricos, lo que dificulta la consulta y aumenta el tamaño del archivo.
- Ausencia total de gobierno de datos: no hay estándares de registro, formatos de fecha, identificadores únicos de cliente o vehículo.
- Riesgo de inconsistencia: diferentes empleados pueden registrar el mismo cliente con nombres distintos, generando silos de información dentro del mismo documento.

### 4.4 Riesgos de aplicaciones

La empresa no cuenta con aplicaciones especializadas para ninguno de sus procesos core:

- Uso de Google Docs como sustituto de un ERP, facturador y gestor de inventario simultáneamente.
- Ausencia de APIs o integraciones: el negocio no puede conectarse con proveedores, pasarelas de pago o plataformas de e-commerce en el futuro próximo sin un rediseño completo.
- Baja escalabilidad: si el negocio crece (más empleados, más sucursales), el modelo actual colapsa inmediatamente.

### 4.5 Riesgos de infraestructura

La infraestructura de soporte tecnológico es mínima y concentrada:

- Dependencia total de la disponibilidad de Google (tercero externo) para operar. Cualquier interrupción del servicio paraliza la operación.
- Sin política de respaldos: no existe proceso documentado de exportación o copia de seguridad del documento principal.
- Sin modo offline: los empleados no pueden operar si no tienen conexión a internet, lo que representa un punto único de falla operacional.
- Ausencia de monitoreo: no hay alertas ante modificaciones no autorizadas, borrados o problemas de sincronización.

### 4.6 Riesgos de seguridad (STRIDE)

El análisis de seguridad mediante metodología STRIDE revela las siguientes amenazas:

- **Spoofing:** cualquier persona con acceso al enlace del documento puede modificar información haciéndose pasar por un empleado legítimo.
- **Tampering:** la información de ventas puede ser alterada sin dejar rastro auditable, exponiéndose a fraudes internos o externos.
- **Repudiation:** sin logs de auditoría, es imposible determinar quién realizó una modificación o eliminación.
- **Information Disclosure:** el documento puede ser compartido accidentalmente, exponiendo información comercial sensible (precios, márgenes, datos de clientes).
- **Denial of Service:** el borrado accidental o malintencionado del documento único destruiría toda la información operacional.
- **Elevation of Privilege:** sin control de roles, cualquier usuario con acceso puede editar, eliminar o copiar toda la información.

### 4.7 Riesgos de gobierno TI

La ausencia de una estructura de gobierno tecnológico es transversal a todos los riesgos identificados:

- No existen estándares documentados para el registro de información ni para la incorporación de nuevas herramientas tecnológicas.
- Las decisiones tecnológicas son reactivas e informales, sin evaluación de impacto arquitectónico.
- No existe un responsable formal de la arquitectura o la seguridad de la información.
- La arquitectura no está documentada; el conocimiento del sistema reside en las personas, no en los procesos.

---

## 5. Arquitectura TO-BE como estrategia de mitigación

### 5.1 Empleados con acceso HTTPS desde cualquier dispositivo

Los 7 empleados acceden desde PCs, laptops o móviles sin instalar software. Todo el tráfico va cifrado desde el origen.

- Elimina la dependencia de un archivo compartido.

### 5.2 Cloud Armor + Identity-Aware Proxy (OAuth 2.0)

Cloud Armor bloquea ataques DDoS, SQL injection y accesos maliciosos. IAP verifica identidad antes de permitir acceso, reemplazando el enlace abierto de Google Docs.

- Resuelve el acceso no autorizado y el problema de las auditorías por brechas de seguridad.
- Elimina una gran cantidad de brechas de seguridad listadas en el análisis STRIDE.

### 5.3 Interfaz web en Cloud Run (autoescalable)

Aplicación web sin gestión de servidores. Escala automáticamente de 1 a N usuarios según demanda.

- Para 7 empleados, el costo base es mínimo.
- Se acaba la dependencia a personas.
- Reduce la desorganización.

### 5.4 API Gateway + 3 microservicios independientes

Inventario, Solicitudes y Facturación son servicios desacoplados. Si Facturación falla, Inventario y Solicitudes siguen funcionando. El API Gateway enruta y protege cada llamada.

- Mitiga los inconvenientes de SPOF.
- Resuelve la falta de inventario.
- Facilita la trazabilidad.

### 5.5 Cloud SQL (PostgreSQL) con réplica y TLS

Base de datos relacional con modelo E-R estructurado, claves foráneas, constraints de integridad, backups automáticos y réplica de lectura para alta disponibilidad.

- Reduce la pérdida de datos y el SPOF.
- Genera backups, lo que permite tener trazabilidad de los datos y un historial.
- Organiza los datos para evitar inconsistencias.

### 5.6 Cloud Storage + Cloud Logging

Cloud Storage guarda adjuntos y backups. Cloud Logging registra toda actividad: quién accedió, qué modificó, desde qué dispositivo y cuándo.

- Facilita la observabilidad de los datos.

---

## 6. Matriz de riesgos consolidada

| ID | Riesgo Identificado | Causa Raíz | Dominio AE | Impacto | Probabilidad | Clasificación | Mitigación Propuesta |
|---|---|---|---|---|---|---|---|
| R-01 | Pérdida o corrupción del documento de ventas (Google Docs único) | Un único archivo concentra todo el historial de ventas sin control de versiones ni respaldo automatizado | Datos / Infraestructura | Crítico | Alta | **Crítico** | Migrar a sistema de base de datos con respaldo automático; establecer política de exportación periódica |
| R-02 | Ausencia de control de inventario estructurado | Gestión visual de bodega sin registro digital de entradas, salidas ni stock mínimo | Procesos / Datos | Alto | Alta | **Crítico** | Implementar módulo de inventario con alertas de stock mínimo y registro de movimientos |
| R-03 | Punto único de falla en gestión de información (dependencia de una persona) | Concentración del conocimiento operativo en uno o pocos empleados sin documentación de procesos | Negocio / Gobierno | Alto | Alta | **Crítico** | Documentar procesos BPMN, capacitar al equipo y distribuir accesos por roles |
| R-04 | Exposición de datos sensibles en Google Docs compartido | Sin control granular de permisos ni cifrado de información comercial y de clientes | Seguridad | Alto | Media | **Alto** | Implementar autenticación por roles, limitar acceso y migrar a solución con gestión de permisos |
| R-05 | Ausencia de trazabilidad en servicios realizados a vehículos | No existe historial digital de diagnósticos, reparaciones ni repuestos utilizados por vehículo | Procesos / Datos | Alto | Alta | **Alto** | Implementar módulo de historial de vehículos vinculado a cliente y servicio |
| R-06 | Falta de sistema de citas y atención al cliente desorganizada | Gestión de citas por canales informales (WhatsApp, llamadas) sin registro centralizado | Procesos / Negocio | Medio | Alta | **Moderado** | Implementar módulo de agendamiento con notificaciones y calendario de servicios |
| R-07 | Errores en facturación manual | Registro de ventas en Google Docs propenso a errores humanos de digitación y duplicidades | Datos / Procesos | Medio | Alta | **Moderado** | Implementar sistema de facturación con validaciones automáticas y numeración consecutiva |
| R-08 | Sin monitoreo ni alertas operacionales | Ausencia total de observabilidad sobre el estado del negocio en tiempo real | Infraestructura / Gobierno | Medio | Alta | **Moderado** | Implementar dashboard de indicadores clave (ventas, inventario, citas pendientes) |
| R-09 | Dependencia de conectividad para acceder a Google Docs | Sin modo offline ni copia local de la información crítica | Infraestructura | Medio | Media | **Moderado** | Aceptación informada: arquitectura TO-BE cloud-first. Se establece procedimiento manual de contingencia para operar durante cortes de conectividad, respaldado por SLA del proveedor ISP. |
| R-10 | Ausencia de auditoría y logs de cambios | Google Docs no provee log de auditoría estructurado sobre quién modifica qué información | Seguridad / Gobierno | Bajo | Media | **Bajo** | Implementar sistema con registro de auditoría por usuario y acción |

---

## 7. Matriz de triage y priorización

| 🔴 RIESGO CRÍTICO — Alta probabilidad + Impacto crítico | 🟠 RIESGO ALTO — Media-Alta probabilidad + Alto impacto |
|---|---|
| **Documento único de Google Docs** — Sin control de acceso · Pérdida total de datos · Dependencia de un solo archivo | **Sin control de inventario · Sin trazabilidad** — Inventario visual · Sin historial de servicios · Gestión de pagos en papel |
| 🟡 **RIESGO MODERADO** — Alta probabilidad + Impacto medio | 🟢 **RIESGO BAJO** — Media probabilidad + Bajo impacto |
| **Capacitación del equipo** — 7 empleados implica capacitaciones para la adopción de la nueva herramienta | **Carga de red · Latencia de microservicios** — Dependencia de internet · Latencia API Gateway |

---

## 8. Modelo Bow-Tie

Se aplica el Modelo Bow-Tie a los riesgos clasificados como críticos y altos (R-01 a R-05), dado que su materialización tendría impacto directo sobre la continuidad operacional del negocio.

### 8.1 R-01 — Pérdida o corrupción del documento de ventas

| CAUSAS (Fuentes de Riesgo) | EVENTO DE RIESGO | EFECTOS (Impacto) |
|---|---|---|
| • Borrado accidental del documento • Modificación no autorizada • Pérdida de acceso a Google Workspace • Cuenta comprometida | Pérdida o corrupción del único repositorio de ventas e información operacional | • Interrupción total de la operación • Pérdida del historial de ventas • Incapacidad para facturar • Daño reputacional con clientes |
| **Controles Preventivos:** • BD con respaldo automático diario • Autenticación individual por rol (IAP + OAuth 2.0) • Control de permisos de escritura | **MITIGACIÓN ESTRUCTURAL** — Migración a sistema de información con BD relacional, backups automáticos y RBAC | **Controles Reactivos:** • Restauración desde respaldo en <1 hora • Modo contingencia en papel para el día • Registro de incidente para auditoría |

### 8.2 R-02 — Ausencia de control de inventario estructurado

| CAUSAS (Fuentes de Riesgo) | EVENTO DE RIESGO | EFECTOS (Impacto) |
|---|---|---|
| • Revisión visual sin registro digital • Sin alertas de stock mínimo • Sin registro de entradas/salidas • Dependencia del conocimiento del bodeguero | Quiebre de stock o sobrestock sin detección oportuna | • Pérdida de ventas por falta de repuestos • Capital inmovilizado en exceso de inventario • Retrasos en servicios comprometidos • Deterioro de la relación con clientes |
| **Controles Preventivos:** • Módulo de inventario con registro de movimientos • Alertas automáticas de stock mínimo • Órdenes de compra desde el sistema | **MITIGACIÓN ESTRUCTURAL** — Servicio de Inventario en Cloud Run con trazabilidad de entradas/salidas y alertas configurables | **Controles Reactivos:** • Revisión manual de bodega como contingencia • Reorden de emergencia a proveedor • Registro del incidente para ajuste de parámetros |

### 8.3 R-03 — Punto único de falla por dependencia de persona clave

| CAUSAS (Fuentes de Riesgo) | EVENTO DE RIESGO | EFECTOS (Impacto) |
|---|---|---|
| • Procesos no documentados • Conocimiento operativo concentrado en 1-2 empleados • Sin distribución de accesos por rol • Equipo reducido de 7 personas | Paralización de operaciones por ausencia del empleado clave | • Incapacidad para registrar ventas o servicios • Errores operativos por personal no familiarizado • Pérdida de confianza del cliente • Riesgo legal por facturación incorrecta |
| **Controles Preventivos:** • Documentación de procesos BPMN digitalizada en el sistema • Distribución de accesos por rol (recepcionista, mecánico, administrador) • Capacitación cruzada del equipo | **MITIGACIÓN ESTRUCTURAL** — Sistema con flujos digitalizados por rol vía IAP + RBAC, eliminando dependencia del conocimiento tácito | **Controles Reactivos:** • Procedimiento manual de contingencia documentado • Escalamiento al administrador del negocio • Registro del incidente para mejora de capacitación |

### 8.4 R-04 — Exposición de datos sensibles en Google Docs compartido

| CAUSAS (Fuentes de Riesgo) | EVENTO DE RIESGO | EFECTOS (Impacto) |
|---|---|---|
| • Sin control granular de permisos • Enlace compartido sin autenticación • Sin cifrado de información comercial • Cuenta de Google sin MFA | Acceso no autorizado a información de clientes, precios y operaciones del negocio | • Exposición de datos de clientes (riesgo legal) • Filtración de precios y márgenes a competencia • Pérdida de confianza de clientes • Posible sanción por incumplimiento de protección de datos |
| **Controles Preventivos:** • Autenticación individual por rol (IAP + OAuth 2.0) • Cloud Armor WAF bloqueando accesos maliciosos • HTTPS end-to-end + TLS en base de datos • RBAC con permisos mínimos por rol | **MITIGACIÓN ESTRUCTURAL** — Migración a sistema con IAP + OAuth 2.0, eliminando el acceso por enlace compartido y estableciendo control granular por usuario | **Controles Reactivos:** • Revocación inmediata de accesos comprometidos • Notificación a clientes afectados • Registro de auditoría en Cloud Logging • Revisión forense del incidente |

### 8.5 R-05 — Ausencia de trazabilidad en servicios realizados a vehículos

| CAUSAS (Fuentes de Riesgo) | EVENTO DE RIESGO | EFECTOS (Impacto) |
|---|---|---|
| • Sin historial digital por vehículo • Registro de ventas no vinculado a cliente ni placa • Sin módulo de diagnósticos ni reparaciones • Dependencia de memoria del mecánico | Imposibilidad de consultar historial de servicios de un vehículo o cliente | • Diagnósticos ineficientes y reprocesos • Incapacidad de ofrecer garantías sobre servicios • Pérdida de fidelización de clientes • Errores en cobro de repuestos ya instalados |
| **Controles Preventivos:** • Módulo de historial vinculado a cliente, vehículo y servicio • Registro obligatorio de diagnóstico y repuestos al cerrar una orden • Consulta de historial disponible para mecánico y recepcionista | **MITIGACIÓN ESTRUCTURAL** — Servicio de Solicitudes con historial estructurado por vehículo en Cloud SQL, vinculado al modelo E-R de clientes y repuestos | **Controles Reactivos:** • Consulta al mecánico de turno como contingencia temporal • Registro manual del servicio para carga posterior al sistema • Revisión periódica de integridad de datos históricos |

---

## 9. Mapa de superficie de riesgo — Almacén Súper Amortiguadores

El siguiente mapa describe los riesgos identificados por capa en la arquitectura actual (AS-IS) y su mitigación en el TO-BE:

| Capa | Riesgos AS-IS | Mitigación TO-BE |
|---|---|---|
| **Capa 1: Interfaz de Usuario (UI)** | Ausencia de interfaz estructurada; actualmente Google Docs no provee UI de negocio. Sin validación de entradas, sin control de sesión, sin UX diferenciada por rol. | Interfaz web en Cloud Run con validación de entradas y sesión por IAP |
| **Capa 2: Lógica de Negocio** | No existe lógica de negocio implementada. Cálculos, alertas de inventario y validaciones se realizan manualmente. Riesgo de errores humanos sistemáticos. | Microservicios con lógica de negocio encapsulada (inventario, solicitudes, facturación) |
| **Capa 3: Datos** | Un único archivo no estructurado como repositorio de datos. Sin integridad referencial, sin tipos de dato, sin consultas, sin respaldos automáticos. Riesgo crítico de pérdida total. | Cloud SQL con modelo E-R, integridad referencial y backups automáticos |
| **Capa 4: Servicios Externos** | Dependencia total de Google Workspace sin SLA empresarial. Sin integración con proveedores, pasarelas de pago ni servicios de notificación. Riesgo de lock-in y baja escalabilidad. | API Gateway + Cloud Armor; arquitectura desacoplada de Google Workspace |

---

## 10. Herramientas y marcos de análisis aplicados

| Herramienta / Marco | Propósito | Aplicación en el Proyecto |
|---|---|---|
| **STRIDE** | Identificación sistemática de amenazas de seguridad | Análisis de las 6 categorías de amenaza sobre el documento Google Docs y la información del negocio |
| **Matriz de Riesgos (Impacto × Probabilidad)** | Priorización visual de riesgos | Clasificación de los 10 riesgos identificados en cuadrantes Crítico, Alto, Moderado y Bajo |
| **Modelo Bow-Tie** | Análisis de causa-evento-efecto con controles preventivos y reactivos | Aplicado a los riesgos críticos R-01 a R-03 y altos R-04 y R-05 |
| **Gap Analysis AS-IS / TO-BE** | Identificar brechas entre estado actual y objetivo | Comparación de capacidades actuales vs. requerimientos de la arquitectura futura |
| **Guía Metodológica AREM (7 dominios)** | Análisis estructurado por dominios de AE | Análisis completo de Negocio, Procesos, Datos, Aplicaciones, Infraestructura, Seguridad y Gobierno TI |
| **BPMN AS-IS** | Modelado de procesos para identificar ineficiencias | Identificación de cuellos de botella en ventas, inventario y atención al cliente |

---

## 11. Conclusiones

El análisis de riesgos arquitectónicos de Almacén Súper Amortiguadores LTDA revela una organización que opera bajo un nivel de riesgo operacional y tecnológico muy alto, derivado principalmente de la ausencia de sistemas de información especializados y de la concentración crítica de datos en una única herramienta de propósito general.

Los hallazgos más relevantes son:

- Tres riesgos clasificados como **CRÍTICOS** que representan amenazas directas a la continuidad del negocio y deben ser atendidos con prioridad máxima en la propuesta TO-BE.
- La ausencia de trazabilidad en servicios compromete la calidad del servicio al cliente y la capacidad de crecimiento del negocio.
- Los riesgos de seguridad son especialmente preocupantes dado que información comercial sensible está expuesta sin controles adecuados.
- La arquitectura futura TO-BE debe abordar simultáneamente los siete dominios analizados para ser verdaderamente resiliente.

---

## Referencias

- Vega, C. A. (2025). *Evaluación de Riesgos Arquitectónicos – Análisis Técnico y Estratégico para la Defensa de Sistemas* [Presentación]. AREM, Universidad de La Sabana.
- *Guía Metodológica para el Análisis de Riesgos en Arquitectura Empresarial – Proyecto Aplicado* (2025). AREM, Universidad de La Sabana.
- IEEE Std 829 – Standard for Software and System Test Documentation.
- OWASP STRIDE Threat Modeling Methodology.
- The Open Group. (2018). *TOGAF Standard, Version 9.2*.
