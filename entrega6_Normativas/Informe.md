# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller 6 - Normativas_

## 👥 Integrantes del equipo
- Valentina Ruiz
- Darek Aljuri
- Santiago Soler

## 🧠 Descripción general del trabajo
Describa brevemente el objetivo del taller y cómo se desarrolló la actividad.

## 🔧 Proceso de desarrollo
Explique cómo realizaron el trabajo: qué decisiones tomaron, qué herramientas utilizaron, qué aspectos modelaron primero y cómo lo fueron ajustando.

## 🧩 Análisis del modelo propuesto
Incluya un análisis sobre:
- Cómo se estructura el modelo entregado
- Cómo representa las necesidades del cliente
- Qué supuestos se tomaron

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
- [1] Apellido, Nombre. *Título*. Año. URL o DOI.
- [2] Fuente oficial BPMN: https://www.omg.org/spec/BPMN/

---

_Este documento hace parte de la entrega del taller X del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
