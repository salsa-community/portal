---
sidebarDepth: 3
tags:
  - vista
  - paradigma
  - enfoque
  - perspectiva
---

# Introducción

![Arquitectura Salsa](/assets/img/salsa-general.png)

## Propósito y Alcance
### Consideraciones inciales

El presente documento, describe los principales elementos que conforman a la arquitectura de software para la plataforma SALSA de CONACyT, fundamentada en los requerimientos, principios, restricciones y metas que la arquitectura del sistema deberá de cumplir. No obstante, se debe advertir que la versión actual del documento de la arquitectura cubre los elementos necesarios y mínimos para cubrir una prueba de concepto de la plataforma, por lo tanto, está sujeta a cambios que se pueden derivar de los hallazgos encontrados durante las pruebas. En su caso, se deberá de genera el documento de recomendaciones de arquitectura, en donde se detalle un plan de evolución de la arquitectura actual a la arquitectura deseada, con una visión a 10 años. Derivado de lo anterior, todos los elementos que se describen en este documento, son susceptibles a evolución y se consideran no completos.

### Arquitectura de software

La arquitectura de software sirve como modelo para el sistema y para el desarrollo del proyecto, ayuda en la definición de las asignaciones de trabajo que deben ser llevadas a cabo por los equipos de diseño e implementación. 
La arquitectura es la principal portadora de cualidades del sistema, tales como el rendimiento, la facilidad de mantenimiento y la seguridad, ninguno de los cuales se puede lograr sin una visión arquitectónica unificadora. 
La arquitectura es un artefacto para el análisis temprano para asegurarse de que un enfoque de diseño proporcionará un sistema aceptable.

### Documento de Arquitectura de Software

El Documento de Arquitectura de Software tiene el objetivo de documentar formalmente la arquitectura de software de la plataforma SALSA, Incluye:

1. Una breve descripción de la arquitectura de software, incluyendo los principales componentes de software y sus interacciones.
2. Un entendimiento común de los conductores (requisitos, restricciones y principios) que influyen en la arquitectura.
3. Una descripción de las plataformas de hardware y software sobre el que está construido y se despliega el sistema.
4. Justificación explícita de cómo la arquitectura satisface los conductores.



### Motivación del Documento de Arquitectura de Software



Como principio rector, el documento de arquitectura de software contiene información complementaria al código y describe aquello que el código en sí no puede hacer. La razón de por qué es necesario el Documento de Arquitectura de Software es porque el código no cuenta toda la historia. 

### Beneficios del Documento de Arquitectura de Software

Los beneficios que provee el Documento de Arquitectura de Software son:

- Una visión compartida colectivamente y una ruta clara que el equipo pueda seguir, por todo el equipo del proyecto.
- Liderazgo técnico y mejor coordinación.
- Poder responder las preguntas relacionadas a decisiones significativas, requerimientos no funcionales, restricciones y otros asuntos transversales.
- Un marco de trabajo para identificar y mitigar los riesgos.
- Consistencia en enfoque y estándares, llevando hacia una base de código estructurada.
- Un conjunto de fundamentos firmes para el resto del proyecto.
- Una estructura con la cual comunicar la solución a diferentes niveles de abstracción hacia diferentes audiencias.
- Mejorar la comunicación entre desarrolladores, administración de la configuración, y área de pruebas de integración al proveer una vista general de la estructura del software.
- Mejorar la extensibilidad al proveer un fundamento flexible sobre el cual se puede extender el software en medida que los requerimientos cambian

### Contenido del Documento de Arquitectura de Software

Las siguientes secciones ilustran el contenido que se debe incluir en un documento de arquitectura de software y la manera de presentar la información desde diferentes puntos de vista considerando a los grupos de interés más comunes. 
Vale la pena señalar que todas estas vistas no son necesariamente requeridas, deberá determinarse su exclusión a partir de factores como el tamaño del proyecto, la complejidad, requerimientos, equipo de trabajo, etc. 
Si la información está disponible en otros lugares, el documento de arquitectura de software debería hacer una referencia a la fuente y no repetirlo (por ejemplo, los requerimientos no funcionales pueden estar presentes en la documentación de requerimientos y los diseños pueden estar en los documentos de diseño separados o un modelo UML). 
El documento de Arquitectura de Software es un documento vivo y dependiendo de su evolución, puede no contener toda la información que aparece aquí en algún momento:

1. Introducción 
2. Acrónimos y Abreviaciones
3. Definición de la Plataforma Sala del CONACyT
4. Premisas de la Arquitectura
5. Vistas Arquitectónicas
    1. Vista de Contexto
    2. Vista Funcional
    3. Vista de Diseño
    4. Vista de Despliegue
    5. Vista Operacional
    6. Vista de Datos
6. Perspectivas de la Arquitectura
    1. Perspectiva de Interoperabilidad
    2. Perspectiva de Seguridad
    3. Perspectiva de Rendimiento
7. Justificación de la Arquitectura

## Audiencia

El Documento de Arquitectura de Software es de interés para todo el equipo de desarrollo del sistema incluyendo los equipos de trabajo de:

* Administración de proyecto
* Requerimientos 
* Arquitectura
* Diseño y construcción
* Pruebas
* Base de Datos
* Seguridad
* Infraestructura 

## Estado

Los estados que puede tener la arquitectura de software de un sistema son:

**Especificada** – Ya se cuenta con los requerimientos arquitectónicos principales,
**En proceso** – Se encuentra en construcción
**Diseñada** – Se encuentra el diseño completo.
**Implementada** – Existe una arquitectura física que se puede ejecutar
**Probada** – Ha pasado la prueba de concepto definida por la CNBV
**En operación** – La arquitectura se encuentra lista para la Fase de Implementación]

## Enfoque Arquitectónico

Los enfoques empleados para el diseño e implementación de la arquitectura de software para la plataforma CONACyT son:

1. Arquitectura orientada a micro servicios
2. Arquitectura de Referencia de Netflix Microservice

### Patrones de Diseño utilizados:

1. Descomposición por capacidades de negocio
2. Descomposición por subdominio
3. Patrón de API Gateway
4. Client-side Discovery
5. Server-side Discovery
6. Circuit breker
7. Access Token

### Vistas que componen a la solución

1. Vista de Contexto
2. Vista Funcional
3. Vista de Diseño
4. Vista de Despliegue
5. Vista Operacional
6. Vista de Datos

### Perspectivas que componen a la solución

1. Perspectiva de Seguridad
2. Perspectiva de rendimiento
3. Perspectiva de Disponibilidad


### Vista de Contexto

La Vista de Contexto de un sistema de software es una de las piezas fundamentales para el diseño de la arquitectura, debido a su naturaleza estrategia y su capacidad inherente de plasmar y transmitir los principales componentes, tanto internos como externos, que conforman al sistema de software general

### Vista Funcional

La Vista de Funcional de un sistema de software es una de las piezas fundamentales para el diseño de la arquitectura, debido a su naturaleza estrategia y su capacidad inherente de plasmar y transmitir los principales componentes funcionales que caracterizan al sistema

### Vista de Diseño

Este producto de trabajo es un modelo UML que describe la realización de los casos de uso y sirve como una abstracción de la vista de implementación y el código fuente. La Vista de Diseño se utiliza como entrada esencial para actividades que se ejecutan durante la implementación del sistema.

### Vista de Despliegue

La Vista de Despliegue, de un sistema de software, muestra los elementos de despliegue del sistema y su relación, de tal manera que se pueda apreciar los elementos que son necesarios para poner en operación al sistema en general

### Vista Operacional

La Vista de Operacional, o vista de operación, es el elemento que permitirá ver como se ejecutará el sistema en el ambiente final del cliente, puntualizando en cómo las personas van a correr, supervisar y administrar el software. La mayoría de los sistemas serán sujetos a requerimientos de soporte y operacionales, particularmente en cómo se supervisan, gestionan y administran.  La inclusión de una sección específica al tema en el documento de arquitectura de software permite ser explícito acerca de cómo su arquitectura apoyará esos requerimientos, particularmente si usted enumera la ayuda del equipo que, en última instancia, va a soportar su sistema.

###  Vista de Datos

La Vista de Datos es un tipo de modelo de datos que determina la estructura lógica de una base de datos y de manera fundamental determina el modo de almacenar, organizar y manipular los datos. Entre los modelos lógicos comunes para bases de datos se encuentran: Modelo jerárquico.

