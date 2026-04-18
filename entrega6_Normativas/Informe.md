# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller 6 - Normativas_

## 👥 Integrantes del equipo
- Valentina Ruiz
- Darek Aljuri
- Santiago Soler

## 🧠 Descripción general del trabajo
El objetivo del taller fue analizar el grado de cumplimiento de los requisitos legales, normativos y de protección de datos aplicables al sistema de información de Súper Amortiguadores LTDA, tomando como base marcos reconocidos como la ISO/IEC 27001, el GDPR, y la normativa colombiana vigente, particularmente la Ley 1581 de 2012 y el principio de Habeas Data.

La actividad se desarrolló mediante la construcción de una lista de verificación estructurada (checklist), en la cual se evaluaron distintos requisitos asociados a la gestión de datos personales, seguridad de la información y gobierno del sistema. Cada elemento del checklist permitió contrastar el estado actual del negocio con lo que exigen las normativas, identificando brechas, controles inexistentes y acciones necesarias.

El resultado obtenido no es únicamente un registro de cumplimiento, sino un instrumento de diagnóstico organizacional que permite orientar la evolución del sistema hacia un modelo alineado con estándares legales y buenas prácticas internacionales, garantizando así la protección de la información y la sostenibilidad del negocio.

## 🔧 Proceso de desarrollo
El desarrollo del trabajo se planteó como un ejercicio de análisis progresivo, partiendo de la realidad actual del negocio hacia el diseño de un sistema futuro que cumpla desde su concepción con las exigencias normativas.

En primer lugar, se identificaron los marcos regulatorios aplicables. Esta selección no fue arbitraria, sino que respondió al contexto del negocio: al manejar datos personales de clientes, la empresa está obligada a cumplir con la legislación colombiana (Ley 1581 y Habeas Data). Adicionalmente, se incorporó ISO 27001 como referencia de buenas prácticas en gestión de seguridad, y GDPR como estándar internacional que fortalece el análisis, incluso si no es obligatorio en este caso.

Posteriormente, se analizó el sistema actual, basado en el uso de Google Docs. Este análisis permitió evidenciar una situación típica de pequeñas empresas: la operación depende de herramientas funcionales, pero carece de controles formales, políticas documentadas y mecanismos de protección estructurados. A partir de esta realidad, se evaluaron aspectos como el manejo del consentimiento, el control de accesos, la confidencialidad de la información y la existencia de responsabilidades definidas.

Una vez comprendido el estado actual, se abordó el sistema propuesto. En este punto, el análisis se enfocó en anticipar los requisitos normativos que deben integrarse desde el diseño del sistema, considerando módulos como inventario, citas, historial de vehículos y autenticación. La decisión clave en esta etapa fue no limitarse a evaluar el cumplimiento actual, sino proyectar cómo debe construirse el sistema para evitar futuros incumplimientos legales.

La información se consolidó en un checklist estructurado, donde cada requisito incluye su referencia normativa, el estado de cumplimiento, la evidencia identificada y una recomendación concreta. Este formato permitió transformar normas abstractas en acciones claras y ejecutables.

Finalmente, se asignaron responsables (Gerencia, Administración y TI), reconociendo que, en el contexto de la empresa, el cumplimiento normativo no recae en un área especializada, sino que debe integrarse dentro de la operación cotidiana.

## 🧩 Análisis del modelo propuesto
El modelo desarrollado presenta una estructura sólida y coherente desde la perspectiva de arquitectura empresarial, en la medida en que traduce marcos normativos complejos en un esquema comprensible, evaluable y accionable para el negocio.

En primer lugar, la estructura del modelo se basa en una lógica de verificación sistemática del cumplimiento. Cada requisito normativo no se presenta de forma aislada, sino contextualizado dentro de la realidad del sistema, acompañado de su estado actual y de una acción recomendada. Esta forma de organización permite que el modelo no sea simplemente descriptivo, sino que funcione como una herramienta de gestión. Es decir, no solo indica qué exige la norma, sino qué está fallando y qué debe hacerse al respecto. Desde el punto de vista metodológico, esto representa una transición importante: el modelo deja de ser teórico y se convierte en operativo.

Adicionalmente, el modelo refleja una comprensión adecuada de la relación entre tecnología, información y regulación. No se limita a evaluar componentes técnicos, sino que incorpora elementos organizacionales como políticas, responsabilidades y procesos. Esto es especialmente relevante en el contexto de la seguridad y el cumplimiento, ya que muchas de las obligaciones legales —como la obtención del consentimiento o la definición de políticas de tratamiento de datos— no dependen únicamente de la tecnología, sino de decisiones organizacionales. En este sentido, el modelo logra capturar la esencia de la arquitectura empresarial: la alineación entre negocio, procesos y tecnología.

En cuanto a la representación de las necesidades del cliente, el modelo demuestra un alto grado de contextualización. Los requisitos no están formulados en términos abstractos o jurídicos complejos, sino que se interpretan en función de situaciones reales del negocio. Por ejemplo, el manejo de datos personales no se analiza únicamente como un principio legal, sino como una práctica concreta que impacta directamente la operación diaria, como el registro de clientes o la gestión de servicios. Esta aproximación facilita que los responsables del negocio comprendan la importancia del cumplimiento normativo y puedan actuar sobre él sin necesidad de intermediación técnica o legal especializada.

Otro aspecto destacable es la proporcionalidad de las recomendaciones. El modelo reconoce que se trata de una empresa pequeña, con recursos limitados y sin un equipo dedicado a seguridad o cumplimiento. Por esta razón, las acciones propuestas no buscan implementar soluciones complejas o costosas, sino establecer controles básicos pero efectivos, como la definición de políticas, la gestión adecuada de accesos o la implementación de mecanismos de respaldo. Esta adecuación al contexto es fundamental, ya que un modelo de cumplimiento que no considere la realidad del negocio difícilmente será implementado.

Por otra parte, el modelo también evidencia una visión prospectiva, al incluir el sistema propuesto dentro del análisis. Esto implica que el cumplimiento normativo no se aborda únicamente como un problema del presente, sino como un criterio de diseño del sistema futuro. Esta decisión es particularmente relevante, ya que permite evitar la acumulación de deuda técnica y legal, asegurando que el nuevo sistema nazca alineado con las exigencias normativas desde su concepción.

Finalmente, en relación con los supuestos del modelo, se identifican varios elementos clave que condicionan el análisis. Se asume, en primer lugar, que el sistema maneja datos personales identificables, lo que activa automáticamente la aplicación de la normativa de protección de datos. Asimismo, se parte de la premisa de que el nivel de madurez en seguridad y cumplimiento es bajo, lo cual se refleja en la ausencia de controles formales y en el estado “Pendiente” de la mayoría de los requisitos. También se asume que el sistema propuesto aún no ha sido implementado, por lo que el modelo funciona como una guía de diseño y no como una auditoría de cumplimiento. Finalmente, se reconoce que la estructura organizacional es limitada, lo que implica que las responsabilidades deben distribuirse entre roles existentes, como la gerencia y la administración.

En conjunto, estos supuestos no debilitan el modelo, sino que lo hacen más realista y aplicable, ya que permiten adaptar el análisis a las condiciones concretas del negocio.

## 📈 Diagrama final entregado
> (Inserte aquí una imagen o enlace al modelo-final.drawio / .asta / PDF)

## 📋 Tabla de actores, entidades o componentes (si aplica)

| Nombre del elemento | Tipo | Descripción | Responsable |
|---------------------|------|-------------|-------------|
| Ej: Paciente        | Actor | Usuario que agenda una cita médica | Cliente |

## 🔍 Investigación complementaria
### Tema investigado:  
Cumplimiento normativo en protección de datos personales y seguridad de la información (ISO/IEC 27001, GDPR, Ley 1581 de 2012 y Habeas Data en Colombia)

---

## 1. Cumplimiento normativo en sistemas de información

El cumplimiento normativo (compliance) en el desarrollo y operación de sistemas de información consiste en asegurar que todos los procesos relacionados con el manejo de datos se ajusten a leyes, regulaciones y estándares aplicables. Esto incluye no solo aspectos técnicos, sino también organizacionales y legales.

En sistemas como plataformas gubernamentales o empresariales, el cumplimiento es especialmente crítico debido a:
- El manejo de grandes volúmenes de datos personales
- La sensibilidad de la información (salud, identidad, finanzas)
- El impacto directo sobre los derechos de los usuarios
- El riesgo reputacional y legal ante incidentes de seguridad

El incumplimiento puede generar sanciones económicas, pérdida de confianza y afectaciones legales.

---

## 2. Ley 1581 de 2012 (Colombia)

La Ley 1581 de 2012 establece el régimen general de protección de datos personales en Colombia, desarrollando el derecho constitucional al Habeas Data.

### 2.1 Principios del tratamiento de datos
- **Legalidad:** El tratamiento debe estar sujeto a la ley
- **Finalidad:** Los datos deben ser recolectados con un propósito específico
- **Libertad:** Se requiere autorización previa del titular
- **Veracidad o calidad:** La información debe ser veraz y actualizada
- **Transparencia:** El titular puede conocer el uso de sus datos
- **Acceso y circulación restringida:** Solo personas autorizadas pueden acceder
- **Seguridad:** Se deben implementar medidas técnicas y administrativas
- **Confidencialidad:** Garantía de reserva de la información

### 2.2 Derechos del titular
- Conocer, actualizar y rectificar sus datos
- Solicitar prueba de la autorización
- Ser informado sobre el uso de sus datos
- Revocar la autorización
- Solicitar la eliminación de sus datos

### 2.3 Obligaciones de las organizaciones
- Obtener consentimiento informado
- Implementar políticas de tratamiento de datos
- Garantizar seguridad de la información
- Reportar incidentes de seguridad
- Permitir el ejercicio de derechos del titular

---

## 3. Habeas Data

El Habeas Data es un derecho fundamental que permite a las personas tener control sobre su información personal.

### Implicaciones en sistemas:
- Implementación de módulos de gestión de datos personales
- Mecanismos para consulta, actualización y eliminación de datos
- Registro de solicitudes realizadas por los usuarios
- Autenticación para validar la identidad del solicitante

---

## 4. ISO/IEC 27001

Es un estándar internacional que define los requisitos para establecer, implementar y mejorar un Sistema de Gestión de Seguridad de la Información (SGSI).

### 4.1 Enfoque basado en riesgos
- Identificación de activos de información
- Evaluación de amenazas y vulnerabilidades
- Definición de controles de seguridad
- Monitoreo y mejora continua

### 4.2 Controles relevantes
- **Control de accesos:** autenticación y autorización
- **Gestión de identidades:** usuarios y roles
- **Cifrado:** protección de datos en tránsito y reposo
- **Seguridad en operaciones:** monitoreo y registros
- **Gestión de incidentes:** respuesta ante brechas
- **Auditoría:** revisión periódica del sistema

### 4.3 Beneficios
- Reducción de riesgos
- Protección de la información
- Cumplimiento legal
- Mejora continua de procesos

---

## 5. GDPR (Reglamento General de Protección de Datos)

El GDPR es una regulación europea que establece altos estándares para la protección de datos personales.

### 5.1 Principios
- Minimización de datos
- Limitación de la finalidad
- Exactitud
- Integridad y confidencialidad
- Responsabilidad proactiva

### 5.2 Derechos del usuario
- Derecho de acceso
- Derecho de rectificación
- Derecho al olvido
- Derecho a la portabilidad
- Derecho a oponerse al tratamiento

### 5.3 Obligaciones
- Consentimiento explícito
- Protección desde el diseño (privacy by design)
- Notificación de brechas de seguridad (≤72 horas)
- Evaluaciones de impacto en privacidad

---

## 6. Seguridad de la información

La seguridad de la información se basa en tres pilares fundamentales:

- **Confidencialidad:** solo acceden usuarios autorizados
- **Integridad:** los datos no son alterados indebidamente
- **Disponibilidad:** la información está accesible cuando se necesita

### Medidas de seguridad:
- Cifrado de datos
- Autenticación multifactor
- Control de accesos por roles
- Monitoreo y logs
- Copias de seguridad
- Políticas de seguridad

---

## 7. Protección contra fugas de datos (Data Loss Prevention - DLP)

Las fugas de datos pueden ocurrir por:
- Ataques cibernéticos
- Errores humanos
- Fallos en configuraciones

### Estrategias de prevención:
- Implementación de DLP
- Restricción de accesos
- Monitoreo de actividad
- Capacitación de usuarios
- Uso de cifrado

---

## 8. Auditoría y trazabilidad

La trazabilidad permite registrar todas las acciones dentro del sistema.

### Elementos clave:
- Logs de acceso
- Registro de cambios en datos
- Historial de actividades
- Monitoreo en tiempo real

Esto facilita:
- Detectar incidentes
- Cumplir auditorías
- Investigar fallos de seguridad

---

## 9. Retención y eliminación de datos

Las organizaciones deben definir políticas claras sobre:

- Tiempo de almacenamiento de datos
- Eliminación segura
- Anonimización de información

Esto evita:
- Acumulación innecesaria de datos
- Riesgos de seguridad
- Incumplimiento normativo

---

## 10. Roles y responsabilidades

### Actores principales:
- **Responsable del tratamiento:** define el uso de los datos
- **Encargado del tratamiento:** procesa los datos
- **Usuarios:** acceso limitado según permisos
- **Administrador de seguridad:** supervisa cumplimiento

---

## 11. Entidades regulatorias en Colombia

Dependiendo del sector, pueden intervenir:

- Superintendencia de Industria y Comercio (SIC)
- Ministerio TIC (MinTIC)
- Ministerio de Salud (MinSalud)
- Superintendencia de Salud
- Superintendencia Financiera

---

## 12. Aplicación al contexto del taller

El uso de estas normativas permite construir un checklist de cumplimiento que evalúe:

- Consentimiento informado
- Seguridad de la información
- Control de accesos
- Auditoría y trazabilidad
- Retención de datos
- Gestión de incidentes

Este análisis permite identificar:
- Cumplimientos actuales
- Brechas de seguridad o legales
- Oportunidades de mejora

---


### Resumen: 
El cumplimiento normativo en sistemas de información implica la adopción de políticas, controles y buenas prácticas que garanticen la protección de los datos personales y la seguridad de la información. Estándares como ISO/IEC 27001 establecen un enfoque basado en la gestión de riesgos para proteger la confidencialidad, integridad y disponibilidad de la información mediante controles como gestión de accesos, cifrado, auditorías y manejo de incidentes. Por otro lado, regulaciones como el GDPR en Europa y la Ley 1581 de 2012 en Colombia (basada en el principio de Habeas Data) establecen obligaciones específicas sobre el tratamiento de datos personales, incluyendo el consentimiento informado, la finalidad del uso de los datos, los derechos del titular (acceso, rectificación y eliminación) y la responsabilidad de las organizaciones frente a incidentes de seguridad.

En el contexto del taller, estas normativas se relacionan directamente con la construcción de un checklist de cumplimiento, ya que proporcionan los criterios que permiten evaluar si un sistema como GobData protege adecuadamente la información que gestiona. Aspectos como el control de accesos, la trazabilidad, la gestión del consentimiento, la retención de datos y la protección contra fugas de información son derivados de estos marcos normativos. Esta investigación permite sustentar la identificación de brechas y la formulación de recomendaciones, asegurando que el sistema no solo funcione correctamente, sino que también cumpla con los requisitos legales y de seguridad exigidos.

## 📚 Referencias
- [1] Congreso de la República de Colombia. *Ley 1581 de 2012: Protección de Datos Personales*. 2012. https://www.funcionpublica.gov.co/eva/gestornormativo/norma.php?i=49981  
- [2] Superintendencia de Industria y Comercio. *Guía para la implementación del principio de responsabilidad demostrada (accountability)*. 2017. https://www.sic.gov.co  
- [3] International Organization for Standardization (ISO). *ISO/IEC 27001: Information Security Management Systems*. 2013. https://www.iso.org/isoiec-27001-information-security.html  
- [4] European Parliament and Council. *General Data Protection Regulation (GDPR) - Regulation (EU) 2016/679*. 2016. https://eur-lex.europa.eu/eli/reg/2016/679/oj  
- [5] Ministerio de Tecnologías de la Información y las Comunicaciones (MinTIC). *Modelo de Seguridad y Privacidad de la Información (MSPI)*. 2020. https://www.mintic.gov.co  
- [6] Superintendencia de Industria y Comercio. *Guía de Protección de Datos Personales en Colombia*. 2020. https://www.sic.gov.co/proteccion-de-datos-personales  
- [7] NIST. *Guide to Protecting the Confidentiality of Personally Identifiable Information (PII)*. 2010. https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf  

---

_Este documento hace parte de la entrega del taller 6 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
