# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller 5 - Evaluación de Seguridad con STRIDE_

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
(Ej: Buenas prácticas BPMN, comparación TOGAF vs C4, principios de seguridad STRIDE, etc.)

### Resumen:
El modelo STRIDE es una metodología de modelado de amenazas utilizada en seguridad informática para identificar posibles vulnerabilidades en sistemas de software durante las etapas de diseño y arquitectura. Este modelo fue desarrollado por Microsoft como parte de su proceso de desarrollo seguro y clasifica las amenazas en seis categorías principales: Spoofing (suplantación de identidad), Tampering (manipulación de datos), Repudiation (repudio de acciones), Information Disclosure (divulgación de información), Denial of Service (denegación de servicio) y Elevation of Privilege (elevación de privilegios). Estas categorías permiten analizar sistemáticamente los componentes de un sistema y detectar posibles riesgos de seguridad antes de que el sistema sea implementado o desplegado.

El modelado de amenazas con STRIDE suele aplicarse sobre diagramas de arquitectura o diagramas de flujo de datos, analizando cada componente del sistema y las interacciones entre ellos para identificar qué tipo de amenaza podría afectar a cada elemento. De acuerdo con la documentación oficial de Microsoft y diversos estudios sobre seguridad de software, esta metodología ayuda a anticipar vulnerabilidades, mejorar el diseño del sistema y definir controles de seguridad adecuados desde etapas tempranas del desarrollo. Entre las buenas prácticas se encuentra analizar cada componente del sistema, identificar las posibles amenazas asociadas y posteriormente definir mecanismos de mitigación que reduzcan el riesgo de ataques.

En el contexto del taller, esta investigación se relaciona directamente con el análisis de seguridad realizado sobre el sistema modelado previamente mediante diagramas de arquitectura. A partir del diagrama de infraestructura y de los componentes del sistema, el equipo aplicó el modelo STRIDE para identificar posibles amenazas de seguridad en cada elemento del sistema, como riesgos de acceso no autorizado, manipulación de información o interrupción del servicio. De esta forma, el ejercicio permitió comprender cómo el modelado de amenazas puede utilizarse para evaluar la seguridad de una arquitectura tecnológica y detectar vulnerabilidades antes de implementar una solución tecnológica.

## 📚 Referencias
- Microsoft Learn. (2023). Threat modeling with STRIDE.
Disponible en: https://learn.microsoft.com/en-us/security/engineering/threat-modeling-stride

- OWASP. (2023). Threat Modeling.
Disponible en: https://owasp.org/www-community/Threat_Modeling

- Carnegie Mellon Software Engineering Institute. (2022). Threat Modeling and STRIDE methodology.
Disponible en: https://insights.sei.cmu.edu/blog/threat-modeling-what-it-is-and-how-to-use-it/

- Threat Modeling: Designing for Security. Shostack, A. (2014). Wiley.

---

_Este documento hace parte de la entrega del taller 5 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
