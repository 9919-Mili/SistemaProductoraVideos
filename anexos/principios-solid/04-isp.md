# Principio de Segregación de Interfaces (ISP)

### Propósito y Tipo del Principio SOLID

Dentro del boceto de clases, se puede observar que algunas clases implementan múltiples responsabilidades que no son relevantes para todos los clientes que las utilizan. Por ejemplo, la clase Sistema expone métodos como gestionar proyectos, gestionar usuarios, notificar usuarios y generar reportes, pero no todos los clientes necesitan acceder a todas estas funcionalidades.
Para solucionarlo se aplicará el Principio ISP (Interface Segregation Principle) para dividir interfaces grandes en interfaces más específicas y cohesivas, de manera que los clientes solo dependan de los métodos que realmente necesitan utilizar.

### Motivación

El boceto actual contiene la clase Sistema que implementa múltiples funcionalidades destinadas a diferentes tipos de usuarios y componentes del sistema. Esta situación genera acoplamiento innecesario, ya que clientes que solo necesitan una funcionalidad específica (como consultar estadísticas) deben depender de una interfaz completa que incluye métodos irrelevantes para su propósito.
Se usará el Principio ISP para crear interfaces especializadas que agrupen métodos relacionados según su contexto de uso, permitiendo que cada cliente dependa únicamente de la interfaz que necesita.

### Explicación de Interfaces 

Una iterfaz es un contrato que define un conjunto de metodos que una clase debe implementar. Te indica que puede hacer, sin detallar como lo hace. 

### Estructura de Clases
[(../diagramas/01-diagrama-clases/01-solid-04-isp.puml)](../diagramas/01-diagrama-clases/01-solid-04-isp.puml)

###s Justifacion tecnica

