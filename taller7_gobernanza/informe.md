# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller 7 Gobernanza_

## 👥 Integrantes del equipo
- Valentina Ruiz Torres (valentinaruito@unisabana.edu.co)
- Santiago Soler Prado (santiagosopr@unisabana.edu.co)
- Darek Aljuri Martinez (darekalma@unisabana.edu.co)

---

## 1. Definir Principios Arquitectónicos

### Datos como Activo Estratégico

Toda información del negocio debe registrarse de forma estructurada en una fuente única, accesible en tiempo real.

**Explicación:** Este principio establece que ningún dato operativo, ya sea una venta, un ingreso de repuesto o una reparación realizada, puede vivir fuera del sistema. No en un cuaderno, no en un Google Docs, no en la memoria de un empleado.

**Justificación en el proyecto:** El problema central de Súper Amortiguadores es exactamente la ausencia de este principio. Hoy toda la operación depende de un único documento manual, lo que genera falta de visibilidad del stock, riesgo de desabastecimiento y ausencia de historial de vehículos. Adoptar este principio obliga a que cada servicio (Inventario, Facturación, Solicitudes) persista sus datos en Cloud SQL PostgreSQL como fuente única de verdad, resolviendo directamente el problema raíz del negocio.



### Modularidad y Separación de Responsabilidades

Cada proceso del negocio (inventario, facturación, solicitudes de servicio técnico) debe estar encapsulado en un servicio independiente con responsabilidades claras y bien delimitadas.

**Explicación:** El sistema no debe construirse como un bloque monolítico sin estructura donde todo está mezclado. Cada dominio del negocio tiene su propia lógica, sus propios datos y su propio ciclo de vida. Un cambio en cómo se factura no debería romper el control de inventario.

**Justificación en el proyecto:** La arquitectura TO-BE refleja directamente este principio: se definen tres servicios independientes desplegados en Cloud Run (Servicio de Facturación, Servicio de Solicitudes, Servicio de Inventario), cada uno con su responsabilidad delimitada. El API Gateway actúa como punto de entrada unificado que enruta las peticiones al servicio correcto, garantizando que los módulos no se llamen directamente entre sí de forma desordenada.



### Trazabilidad Total de las Operaciones

Cada transacción relevante debe quedar registrada con fecha, responsable y estado. Ninguna operación crítica puede ocurrir sin dejar rastro en el sistema.

**Explicación:** La trazabilidad convierte el sistema en la memoria institucional de la empresa. Permite auditorías, resolución de disputas con clientes y análisis histórico del negocio.

**Justificación en el proyecto:** La arquitectura TO-BE incluye explícitamente **Cloud Logging** como componente de auditoría y monitoreo. Esto no es accidental: cada operación que pase por el API Gateway y los servicios quedará registrada. Hoy la empresa no sabe qué se vendió hace tres meses, qué técnico atendió un vehículo específico ni cuándo se realizó cierta reparación. Cloud Logging resuelve directamente este problema a nivel de infraestructura.

---

## 2. Definir Estándares

### Lenguaje y Framework

**Selección:** JavaScript (Node.js con Express) para backend + React.js para frontend

Para el backend se adopta JavaScript con Node.js y Express porque permite construir APIs REST livianas y eficientes, es el mismo lenguaje que el frontend (reduciendo la carga cognitiva del equipo), y tiene un ecosistema maduro de librerías para conexión con PostgreSQL. Cada uno de los tres servicios (Facturación, Solicitudes, Inventario) se implementa como una aplicación Node.js independiente, desplegada en su propio contenedor de Cloud Run.

Para el frontend se adopta React.js porque permite construir interfaces dinámicas como tablas de inventario, formularios de registro de servicios y dashboards de ventas sin requerir recargas completas de página. La app web se despliega también en Cloud Run como se muestra en el diagrama TO-BE.

**Razón para este proyecto:** Usar JavaScript tanto en backend como en frontend unifica el stack del equipo, reduce la fragmentación tecnológica y facilita el onboarding de nuevos desarrolladores. Node.js es además especialmente eficiente para servicios de API con múltiples peticiones concurrentes, lo cual es relevante cuando varios empleados del taller (recepción, mecánico, administrador) usan el sistema simultáneamente.



### Base de Datos

**Selección:** Cloud SQL con PostgreSQL (base de datos relacional gestionada por Google Cloud)

PostgreSQL garantiza integridad transaccional ACID, lo que significa que operaciones críticas como descontar stock al momento de facturar ocurren de forma atómica: o se completan totalmente o no se registran en absoluto. Cloud SQL agrega sobre esto gestión automática de backups, alta disponibilidad y escalado sin necesidad de administrar el servidor de base de datos manualmente.

El modelo relacional es el más natural para los datos del negocio, ya que las entidades tienen relaciones claras entre sí: un cliente tiene múltiples vehículos, un vehículo tiene múltiples órdenes de servicio, una orden contiene múltiples repuestos con sus precios y cantidades.

**Razón para este proyecto:** Una base de datos NoSQL sería inadecuada porque la flexibilidad de esquema que ofrece no se necesita, los datos del negocio son estructurados y predecibles  y la consistencia eventual que acepta es inaceptable para transacciones de facturación. Cloud SQL además se integra nativamente con los servicios Cloud Run


### Tipo de Comunicación

**Selección:** REST API sobre HTTPS (externa) + TCP/TLS (interna hacia base de datos)

La comunicación entre el frontend y los servicios del backend se realiza mediante REST sobre HTTPS, enrutada a través del API Gateway. Cada servicio expone sus operaciones como endpoints bien definidos: GET /inventario/productos/, POST /facturacion/facturas/, GET /solicitudes/ordenes/{id}/, etc.

La comunicación entre los servicios Cloud Run y la base de datos Cloud SQL ocurre sobre TCP/TLS en el puerto 5432, garantizando que los datos en tránsito estén siempre cifrados, incluso dentro de la red interna de Google Cloud.

Se descarta la comunicación asíncrona basada en eventos (Kafka, Pub/Sub) porque la complejidad de un sistema de mensajería distribuida no está justificada para el volumen y las necesidades actuales del negocio. No hay procesos que necesiten desacoplamiento asíncrono en esta etapa.

**Razón para este proyecto:** REST es el estándar más comprensible, depurable y documentado. El API Gateway centraliza el enrutamiento y la seguridad, de forma que ningún servicio necesita implementar autenticación de forma individual.

---

### Infraestructura y Despliegue

**Selección:** Google Cloud Platform — Cloud Run + Cloud SQL + Cloud Armor + Cloud Storage + Cloud Logging

La arquitectura TO-BE se despliega completamente sobre Google Cloud con los siguientes componentes:

| Componente | Servicio GCP | Rol |
|---|---|---|
| Protección y autenticación | Cloud Armor / IAP / WAF | Primera línea de seguridad antes de llegar a la aplicación |
| App Web (interfaz) | Cloud Run | Sirve el frontend React.js |
| API Gateway | API Gateway REST/HTTPS | Enruta peticiones a los servicios correctos |
| Servicio Facturación | Cloud Run | Lógica de facturación (Node.js) |
| Servicio Solicitudes | Cloud Run | Lógica de órdenes de servicio (Node.js) |
| Servicio Inventario | Cloud Run | Lógica de inventario (Node.js) |
| Base de Datos | Cloud SQL PostgreSQL | Persistencia central con integridad ACID |
| Archivos y backups | Cloud Storage | Fotos de diagnóstico, documentos escaneados, backups |
| Auditoría y monitoreo | Cloud Logging | Registro de todas las operaciones del sistema |

**Razón para este proyecto:** Cloud Run es especialmente adecuado para este caso porque permite desplegar contenedores sin administrar servidores, escala automáticamente a cero cuando no hay tráfico (reduciendo costos en horarios fuera del taller) y escala hacia arriba cuando múltiples empleados usan el sistema simultáneamente. Cloud Armor protege el sistema de ataques externos desde el primer día sin configuración compleja.

---

## 3. Decisiones Arquitectónicas (ADR)

### ADR #001 – Adopción de Servicios Independientes en Cloud Run por Dominio de Negocio

#### Descripción del Problema

El sistema debe digitalizar los procesos del negocio: gestión de inventario, órdenes de servicio técnico y facturación. 

Construirlo sin ninguna estructura generaría exactamente el mismo problema que hoy tiene la empresa con su Google Docs: un único punto de caos donde todo depende de todo. Sin embargo, el equipo también debe evitar una distribución tan compleja que sea imposible de operar para una PyME. El TO-BE del proyecto propone una solución intermedia: tres servicios claramente delimitados por dominio, cada uno desplegado de forma independiente en Cloud Run, comunicados a través de un API Gateway central.

#### Alternativas Evaluadas

**Opción A – Monolito único en Cloud Run:** Todo el código (inventario, facturación, solicitudes) en un único servicio. Simple de desplegar, pero cualquier cambio en un módulo requiere redesplegar todo el sistema y un fallo afecta todos los dominios simultáneamente.

**Opción B – Microservicios con comunicación directa entre sí:** Cada servicio llama directamente a los otros por red cuando los necesita. Máxima autonomía, pero genera dependencias ocultas y fallos en cascada: si el servicio de inventario cae, facturación también falla.

**Opción C – Servicios independientes por dominio con API Gateway central:** Cada dominio (Facturación, Solicitudes, Inventario) es un servicio Cloud Run independiente. El API Gateway es el único punto de entrada desde el exterior. Los servicios no se llaman directamente entre sí; toda petición entra por el Gateway. Cada servicio escala de forma independiente según su carga.

#### Decisión Tomada

La opción C tal como refleja el diagrama TO-BE del proyecto. El API Gateway centraliza el enrutamiento, la autenticación y el control de acceso, mientras que cada servicio Cloud Run se enfoca exclusivamente en su dominio de negocio. Esto es coherente con el principio de Modularidad: un cambio en la lógica de facturación no requiere tocar el servicio de inventario, y ambos pueden escalar de forma independiente.

#### Consecuencias

**(+) Positivas:**
- Cada servicio puede desplegarse, actualizarse y escalarse de forma independiente sin afectar a los demás.
- Un fallo en el Servicio de Solicitudes no tumba Facturación ni Inventario.
- Cloud Run escala automáticamente cada servicio según la demanda real, optimizando costos.
- El API Gateway centraliza la seguridad: ningún servicio necesita implementar autenticación individualmente.

**(−) Negativas (trade-offs asumidos):**
- La depuración de errores es más compleja que en un monolito: un error puede involucrar múltiples servicios y logs distribuidos (mitigado con Cloud Logging centralizado).
- El equipo debe disciplinarse para no crear dependencias directas entre servicios que rompan la independencia arquitectónica.
- El costo operacional es mayor que un monolito único, aunque Cloud Run mitiga esto con escalado a cero en horarios sin uso.



### ADR #002 – Cloud SQL PostgreSQL como Base de Datos Central Compartida por Todos los Servicios

#### Descripción del Problema

Hoy la empresa gestiona toda su información en un Google Docs compartido de forma manual. Esto produce tres problemas críticos:

Primero, no hay integridad entre los datos: una factura puede registrarse sin que el inventario se descuente. Segundo, no hay historial estructurado: no es posible saber qué se vendió el mes pasado ni qué técnico atendió un vehículo. Tercero, no hay control de concurrencia: si dos personas editan el documento al mismo tiempo, los datos se corrompen.

Adicionalmente, con tres servicios independientes (Facturación, Solicitudes, Inventario), surge la pregunta de si cada servicio debe tener su propia base de datos aislada o si todos comparten una base de datos central.

#### Alternativas Evaluadas

**Opción A – Una base de datos por servicio (aislamiento total):** Máxima independencia entre servicios. Sin embargo, las consultas que cruzan dominios (ej. una factura que necesita verificar stock) requieren llamadas entre servicios o mecanismos de sincronización complejos que no están justificados para el tamaño del negocio.

**Opción B – Google Sheets con automatizaciones (Apps Script):** Mínima inversión inicial. Sin embargo, no ofrece control transaccional, las relaciones entre entidades son frágiles y el riesgo de pérdida de integridad es alto. No resuelve el problema raíz.

**Opción C – Cloud SQL PostgreSQL compartido, con esquemas separados por dominio:** Una única instancia de Cloud SQL a la que acceden los tres servicios, pero cada dominio opera sobre su propio esquema (inventario, facturacion, solicitudes). Integridad referencial cruzada disponible cuando se necesita, con la simplicidad de administrar una sola base de datos.

#### Decisión Tomada

La opción C, coherente con el diagrama TO-BE que muestra una única instancia de Cloud SQL PostgreSQL conectada a los tres servicios Cloud Run. Todas las entidades del sistema se modelan con relaciones explícitas. Cloud Storage complementa esta decisión para el almacenamiento de archivos binarios (fotos de diagnóstico, documentos escaneados) que no deben vivir en la base de datos relacional, resolviendo el trade-off que tendría una base de datos SQL pura.

#### Consecuencias

**(+) Positivas:**
- Integridad referencial garantizada: no puede existir una factura sin cliente, ni un ítem de factura sin producto existente en inventario.
- Historial auditable y completo de todas las transacciones, resolviendo directamente la falta de trazabilidad actual.
- Cloud SQL gestiona automáticamente backups, actualizaciones de seguridad y alta disponibilidad sin administración manual del servidor.
- Cloud Storage resuelve el almacenamiento de archivos adjuntos (fotos de diagnóstico, documentos), complementando lo que PostgreSQL no maneja bien.

**(−) Negativas (trade-offs asumidos):**
- Una única instancia de base de datos es un punto de dependencia compartido entre los tres servicios: si Cloud SQL tiene problemas, los tres servicios se ven afectados (mitigado por la alta disponibilidad gestionada de Cloud SQL).
- El esquema relacional es menos flexible ante cambios estructurales frecuentes: agregar una nueva relación requiere una migración coordinada entre servicios.
- El equipo debe tener conocimiento básico de diseño relacional, SQL y manejo de Sequelize para aprovechar correctamente las capacidades del motor.
