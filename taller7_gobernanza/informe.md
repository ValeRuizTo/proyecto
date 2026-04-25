# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller 1 - [BPMN]_

## 👥 Integrantes del equipo
- Valentina Ruiz Torres (valentinaruito@unisabana.edu.co)
- Santiago Soler Prado (santiagosopr@unisabana.edu.co)
- Darek Aljuri Martinez (darekalma@unisabana.edu.co)

## 🧠 Descripción general del trabajo

El objetivo del taller fue modelar un proceso de negocio real del cliente utilizando la notación BPMN, identificando claramente los eventos, actividades, decisiones, actores involucrados y puntos críticos del flujo.

El proceso seleccionado corresponde a la gestión de inventario y venta de repuestos de la empresa ******* ubicada en el 7 de agosto en bogota. Este proceso inicia cuando un cliente solicita un repuesto y finaliza cuando el producto es entregado y facturado, o cuando se gestiona el pedido al proveedor en caso de no contar con disponibilidad.

La actividad se desarrolló mediante el análisis del flujo real descrito por la empresa, identificando las etapas principales, los responsables del proceso y las decisiones que afectan el flujo (por ejemplo, la verificación de disponibilidad del inventario). Posteriormente, el proceso fue estructurado en un modelo BPMN digital que representa gráficamente la secuencia lógica de actividades y puntos de decisión.

## 🔧 Proceso de desarrollo

Para realizar el trabajo, primero analizamos el proceso actual descrito por la empresa:

- Los repuestos se encuentran almacenados en la bodega.
- El cliente solicita un repuesto específico.
- Se verifica si el producto está disponible en inventario (ya sea físicamente en bodega o mediante el conocimiento estimado de “Felipe”).
- Si el producto está disponible, se realiza el cambio o venta y se genera la facturación.
- Si el producto no está disponible, se solicita al proveedor.

Decisiones tomadas

- Se identificó como evento inicial la solicitud del cliente.
- Se modeló como una decisión: ¿El producto está disponible en inventario?
- Se diferenciaron claramente los actores: Cliente, Encargado de inventario/Bodega (Felipe) y Proveedor.
- Se definió como evento final la facturación y entrega del producto o la generación del pedido al proveedor.

Herramientas utilizadas

Se utilizo drwai.io como herramienta de modelado

## 🧩 Análisis del modelo propuesto
Incluya un análisis sobre:
- Cómo se estructura el modelo entregado
    - Evento de inicio: Solicitud del cliente.
    - Tarea: Verificar disponibilidad del repuesto en bodega.
    - Compuerta exclusiva: ¿El producto está disponible?
    - Sí: Realizar cambio/venta → Facturar → Entregar producto → Evento final.
    - No: Solicitar producto al proveedor → Esperar entrega → Notificar al cliente (opcional según alcance) → Evento final.
  
- Cómo representa las necesidades del cliente

El modelo representa adecuadamente las necesidades del cliente porque:
  - Refleja el flujo real descrito por la empresa.
  - Incluye la verificación de inventario como punto clave del proceso.
  - Contempla ambos escenarios posibles: disponibilidad o no del producto.
  - Muestra la interacción con el proveedor cuando es necesario.

El control del inventario depende en parte del conocimiento de una persona “Felipe”, lo cual puede generar riesgos si no existe un sistema formal de control.
  
- Qué supuestos se tomaron

   - Que la solicitud del cliente es clara y contiene la referencia correcta del repuesto
   - Que el proceso de facturación se realiza inmediatamente después de confirmar disponibilidad en el inventario
   - Que el pedido al proveedor se gestiona de manera directa y sin procesos adicionales complejos
   - Que el tiempo de espera por parte del proveedor es indefinido 

## 📈 Diagrama final entregado

![.](BPMN.drawio.png)


## 📋 Tabla de actores, entidades o componentes (si aplica)

| Nombre del elemento     | Tipo              | Descripción                                                             | Responsable        |
| ----------------------- | ----------------- | ----------------------------------------------------------------------- | ------------------ |
| Cliente                 | Actor             | Persona que solicita el diagnóstico o repuesto y realiza el pago        | Cliente            |
| Empleado / Vendedor     | Actor             | Persona que revisa inventario, gestiona solicitudes y coordina la venta | Empresa            |
| Proveedor               | Actor externo     | Empresa que suministra la pieza cuando no está disponible en inventario | Proveedor          |
| Solicitud / Diagnóstico | Evento          | Requerimiento inicial realizado por el cliente                          | Cliente / empleado (dependiendo del caso)           |
| Inventario              | Entidad           | Stock de piezas disponibles en la bodega                                | Empleado / Empresa |
| Pieza o Repuesto        | Entidad           | Producto solicitado por el cliente                                      | Empresa            |
| Solicitud de pieza      | Evento         | Pedido realizado al proveedor cuando no hay existencia                  | Empleado           |
| Factura                 | Evento         | Documento que formaliza la venta del producto                           | Empresa            |
| Recepción de pieza      | Evento            | Confirmación de llegada del producto desde el proveedor                 | Empleado           |

## 🔍 Investigación complementaria
### Tema investigado: Buenas prácticas BPMN

### Resumen:
Las mejores prácticas de modelamiento BPMN según Bizagi Modeler se basan en cuatro principios principales: mantener una secuencia lógica y clara, utilizar correctamente el estándar BPMN, nombrar adecuadamente los elementos y simplificar los diagramas. En primer lugar, se recomienda que todo proceso tenga eventos de inicio y fin explícitos, que el flujo siga una dirección consistente (usualmente de izquierda a derecha) y que el camino principal sea fácilmente identificable antes de agregar escenarios alternativos o excepciones. También se enfatiza conservar un formato visual uniforme, evitar cruces innecesarios de conectores y distinguir entre finales exitosos y no exitosos. El objetivo es que cualquier lector pueda comprender rápidamente la lógica del proceso sin ambigüedades ni sobrecarga visual.

En segundo lugar, Bizagi destaca la importancia de respetar el uso formal del estándar BPMN, verificando la correcta aplicación de contenedores, carriles (lanes), actividades, compuertas y conectores. Esto implica no dibujar flujos fuera de los límites del proceso, no mezclar tareas entre carriles, utilizar compuertas para decisiones en lugar de tareas, balancear bifurcaciones y sincronizaciones, y diferenciar correctamente los flujos de secuencia (dentro del mismo proceso) de los flujos de mensaje (entre procesos distintos). Asimismo, se recomienda nombrar claramente los elementos actividades con verbo + objeto, procesos con descripciones completas y compuertas con condiciones o preguntas y simplificar los diagramas integrando tareas consecutivas del mismo actor, utilizando subprocesos embebidos o reutilizables para agrupar actividades relacionadas, aplicando patrones de proceso existentes y dejando los detalles menores en documentación externa. Estas prácticas buscan diagramas limpios, consistentes y fáciles de comunicar, que sirvan tanto para análisis como para mejora o futura automatización.

La relación con el Taller es directa, ya que el ejercicio de modelar el agendamiento de citas de la Clínica replica un escenario real del sector salud, uno de los ejemplos industriales más comunes de BPMN, asi mismo se podria decir que este puede ser aplicado a cualquier industria que busque estandarizar sus procesos y identificar áreas de mejora. Al aplicar buenas prácticas como identificar correctamente eventos de inicio y fin, actividades principales, gateways de disponibilidad y roles mediante lanes el equipo no solo cumple con la rúbrica de claridad y simbología correcta, sino que desarrolla un modelo que puede adaptarse posteriormente al cliente real asignado. De esta manera, la investigación sobre buenas prácticas y ejemplos sectoriales se convierte en un respaldo metodológico que conecta la teoría con la práctica del taller, demostrando que BPMN es una herramienta aplicable en contextos profesionales reales y no solo académicos.

## 📚 Referencias
- [1] ¿Qué es BPMN? Miro Help Center. Disponible en: https://miro.com/es/diagrama/que-es-bpmn/
- [2] Bizagi, Best Practices in Process Modeling. Bizagi Help Platform. Disponible en: https://help.bizagi.com/platform/es/index.html?best_practices_in_modeling.htm
- [3] OpenAI, ChatGPT — modelo de lenguaje grande entrenado por OpenAI, Fuente asistida por IA: ChatGPT, Febrero 2026.
- [4] Fuente oficial BPMN: https://www.omg.org/spec/BPMN/

---

_Este documento hace parte de la entrega del taller X del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
