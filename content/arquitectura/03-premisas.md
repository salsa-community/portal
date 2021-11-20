---
tags:
  - salsa
  - plataforma
---


# Premisas de la Arquitectura

## Contexto general

La arquitectura que se desea desarrollar es mayormente una aplicación empresarial del lado del servidor. Debe admitir una variedad de diferentes clientesm, incluidos: navegadores de escritorio, navegadores móviles y aplicaciones móviles nativas, enfatizando fuertemente en la comunicación máquina a máquina con sistemas legados del CONACyT. La aplicación también debe exponer una API para ser consumida por terceros. También podría integrarse con otras aplicaciones a través de servicios web o un intermediario de mensajes. La aplicación maneja las solicitudes (solicitudes y mensajes HTTP) mediante la ejecución de la lógica de los aplictivos del CONACyT; acceder a una base de datos; intercambiar mensajes con otros sistemas (MIIC, People Soft, Seminuevos); y devuelve una respuesta HTML / JSON. Existen componentes lógicos correspondientes a diferentes áreas funcionales de la aplicación.

## Necesidades

## Restricciones

El software vive dentro del contexto del mundo real y el mundo real tiene restricciones. Esta sección permite indicar estas restricciones por lo que queda claro que se está trabajando dentro de estas y es obvio cómo afectan a las decisiones de arquitectura.  Las restricciones se imponen generalmente a usted, por lo general por la organización o cliente que ha pedido el sistema de software a construir. Beneficios de las restricciones Las restricciones pueden ser impuestas sobre la arquitectura, pero no todas son malas. En palabras de TS Eliot, 
> _"Cuando se le obliga a trabajar dentro de un marco estricto, la imaginación se pone a prueba al máximo y producirá sus ideas más ricas. Dada la libertad total, es probable que el trabajo se expanda"  -TS Eliot-_ 

Da a alguien una semana para hacer una tarea y esa tarea se llevará una semana. Dales dos semanas y esa misma tarea se llevará en dos semanas. Sin restricciones, a menudo hay un número infinito de maneras de resolver el problema. La reducción del número de opciones disponibles a menudo hace su trabajo más fácil el diseño de software. Tales restricciones tienen el poder de influir en forma masiva la arquitectura, sobre todo si limitan la tecnología que se puede utilizar para generar la solución. Si las restricciones tienen un impacto, vale la pena resumirlos (por ejemplo, qué son, por qué están siendo impuestas y que les está imponiendo) y diciendo cómo son significativos a su arquitectura. De este modo impide que tenga que responder a preguntas sobre por qué ha tomado algunas decisiones aparentemente estrafalarias. 

### Restricciones organizacionales


Las restricciones organizacionales que influyen en el diseño de la arquitectura del sistema son:
La tecnología que se puede utilizar es la especificada en el Anexo Técnico del cliente, la cual es su mayoría es tecnología de Microsoft
Se deberá de ajustar el esfuerzo al Tiempo, presupuesto y recursos cotizados
El equipo de desarrollo es nuevo utilizando tecnologías de Microsoft Azure
El proyecto tiene una naturaleza estratégica y de alto valor para el cliente

### Restricciones técnicas


- El desarrollo se deberá de acotar a las tecnologías establecidas en el Anexo Técnico
- Se deberá de diseñar servicios para interoperabilidad utilizando el lenguaje de especificaciones de API de la industria (Swagger 2.0 u Open API 3.0)
- La interoperabilidad deberá de ser en todo momento a través de Web Services REST FULL. 

Lenguajes de programación a utilizar:
- Capa Servidor: java, python, javascript
- Capa de Base de Datos: Base de datos PostgreSQL o alguna que no genere costos por la licencia



