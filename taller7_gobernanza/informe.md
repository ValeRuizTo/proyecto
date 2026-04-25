# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller 7 Gobernanza_

## 👥 Integrantes del equipo
- Valentina Ruiz Torres (valentinaruito@unisabana.edu.co)
- Santiago Soler Prado (santiagosopr@unisabana.edu.co)
- Darek Aljuri Martinez (darekalma@unisabana.edu.co)

## 1. Definir Principios Arquitectónicos
- Definir mínimo 3 principios, Explicar cada uno y Justificar su uso en el proyecto
  
    - **Datos como Activo Estratégico**
      
Toda información del negocio debe registrarse de forma estructurada en una fuente única, accesible en tiempo real. Explicación: Este principio establece que ningún dato operativo, ya sea una venta, un ingreso de repuesto o una reparación realizada  puede vivir fuera del sistema. No en un cuaderno, no en un Google Docs, no en la memoria de un empleado.

Justificación en el proyecto: El problema central de Súper Amortiguadores es exactamente la ausencia de este principio. Hoy toda la operación depende de un único documento manual, lo que genera falta de visibilidad del stock, riesgo de desabastecimiento y ausencia de historial de vehículos. Adoptar este principio obliga a que cada módulo (inventario, clientes, servicios) persista sus datos de forma estructurada, resolviendo directamente el problema raíz del negocio.

   - **Modularidad y Separación de Responsabilidades**
    
Cada proceso del negocio (inventario, facturación, clientes, servicios técnicos) debe estar encapsulado en un módulo independiente con responsabilidades claras y bien delimitadas. El sistema no debe construirse como un bloque monolítico sin estructura donde todo está mezclado. Cada dominio del negocio tiene su propia lógica, sus propios datos y su propio ciclo de vida. Un cambio en cómo se factura no debería romper el control de inventario.

Justificación en el proyecto: Súper Amortiguadores tiene al menos cuatro procesos claramente diferenciados: venta de repuestos, diagnóstico, reparación y facturación. Si estos procesos se implementan de forma entrelazada, cualquier modificación futura se vuelve costosa y riesgosa. La modularidad permite que el negocio crezca o cambie un proceso sin afectar los demás, algo crítico para una empresa que está digitalizándose por primera vez.

 - **Trazabilidad Total de las Operaciones**
   
Cada transacción relevante debe quedar registrada con fecha, responsable y estado. Ninguna operación crítica puede ocurrir sin dejar rastro en el sistema. La trazabilidad convierte el sistema en la memoria institucional de la empresa. Permite auditorías, resolución de disputas con clientes y análisis histórico del negocio.

Justificación en el proyecto: Hoy la empresa no sabe qué se vendió hace tres meses, qué técnico atendió un vehículo específico ni cuándo se realizó cierta reparación. Este principio resuelve directamente la "ausencia de un historial estructurado de los vehículos" mencionada en el problema, y es además un requisito implícito de cualquier sistema de facturación serio.

## 2. Definir Estándares
- Lenguaje o framework, Tipo de comunicación (REST, eventos)

 - **Lenguaje y Framework**
Selección: JavaScript para backend + React.js (frontend)

Para el backend se adopta JavaScript   facilita el manejo de la base de datos sin escribir SQL manualmente, un sistema de autenticación y roles listo para usar, y una estructura de proyecto que naturalmente favorece la separación por módulos (inventario, clientes, servicios, facturación), lo cual es coherente con el principio de Modularidad definido anteriormente. Además,  REST Framework permite exponer los datos como API de forma sencilla.

Para el frontend se adopta React.js porque permite construir interfaces dinámicas como tablas de inventario, formularios de registro de servicios y dashboards de ventas sin requerir recargas completas de página, mejorando la experiencia del usuario en el mostrador del almacén.

Razón para este proyecto: El equipo técnico de una empresa en etapa de digitalización inicial necesita un stack maduro, con documentación abundante y una comunidad activa. Python y React cumplen ambas condiciones, reducen la curva de aprendizaje y permiten avanzar rápido sin sacrificar calidad estructural.


 - **Base de Datos**
   
Selección: PostgreSQL (base de datos relacional)

PostgreSQL garantiza integridad transaccional ACID, lo que significa que operaciones críticas como descontar stock al momento de facturar ocurren de forma atómica: o se completan totalmente o no se registran en absoluto. Esto elimina el riesgo de inconsistencias que hoy existen en el Google Docs manual, donde una venta puede registrarse sin que el inventario se actualice.
El modelo relacional es además el más natural para los datos del negocio, ya que las entidades tienen relaciones claras entre sí: un cliente tiene múltiples vehículos, un vehículo tiene múltiples órdenes de servicio, una orden contiene múltiples repuestos con sus precios y cantidades.

Razón para este proyecto: Una base de datos NoSQL sería inadecuada aquí porque la flexibilidad de esquema que ofrece no se necesita — los datos del negocio son estructurados y predecibles — y la consistencia eventual que acepta es inaceptable para transacciones de facturación.

 - **Tipo de Comunicación**

Selección: REST API sobre HTTP/JSON (comunicación síncrona)

La comunicación entre el frontend (React) y el backend (JavaScript) se realiza mediante APIs REST. Cada módulo del sistema expone sus operaciones como endpoints bien definidos: GET /inventario/productos/, POST /servicios/ordenes/, GET /facturacion/facturas/{id}/, etc.

Se descarta por ahora la comunicación asíncrona basada en eventos (Kafka, RabbitMQ) porque, como establece el principio de Simplicidad Operacional, la complejidad de un sistema de mensajería distribuida no está justificada para el volumen y las necesidades actuales del negocio. No hay procesos que necesiten desacoplamiento asíncrono en esta etapa: cuando un técnico registra una reparación, el sistema puede responder síncronamente sin problema.

Razón para este proyecto: REST es el estándar más comprensible, depurable y documentado. Cualquier desarrollador que se integre al equipo en el futuro entenderá inmediatamente cómo funciona la comunicación del sistema, sin necesidad de conocer brokers de mensajes ni patrones de eventos.

