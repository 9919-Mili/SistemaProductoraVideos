# Principio Abierto/Cerrado (OCP)

## Proposito y Tipo del Principio Solid

Dentro del boceto de clases, se puede ver que clases varias clases estan abiertas a modificación al poseer atributos asociados directamente a una clase concreta.

Para solucionarlo se aplicara el Principio OCP para crear una clase intermediaria a las que se releve la relación directa con la clase concreta de donde se toma la información, asi no se modificara la clase principal sino la clase intermediaria.

## Motivación

El boceto actual contiene la clase Usuario, que ante cualquier modificación tambien se necesitara modificar las clases Proyecto, Etapa y Comentario que poseen atributos directamente relacionados a la clase Usuario, por lo tanto abiertas a modificación.

Se usara el Principio OCP para crear una interfaz intermedia encargada de obtener la información de la clase Usuario mediante una extensión que facilite cambios e implementaciones futuras sin modificar las clases principales.

## Explicación de Herencia

Una relación de herencia en el diseño orientado a objetos es un vínculo entre una clase base (superclase) y una clase derivada (subclase), donde la subclase hereda atributos y métodos de la superclase. Esto permite reutilizar código y extender las funcionalidades de la superclase.

Su aplicación a OCP, se da en como la herencia permite que una clase esté abierta para extensión ( crear nuevas subclases con comportamientos adicionales o modificados) pero cerrada para modificación (no es necesario cambiar el código de la clase base). Así, se usara para crear una clase interfaz que proveera sus funcionalidades a la clase Usuario, de esta manera se "aislaran" las modificaciones de la clase Usuario y podran implementarse otras clases similares a Usuario que tambien esten extendidas por la superclase.

## Estructura de Clases

- [Diagrama_Principio_OCP](/diagramas/01-diagrama-clases/01-solid-02-ocp.png)

![Diagrama_UML_Principio](/diagramas/01-diagrama-clases/01-solid-02-ocp.png)

## Justificación Técnica

El diagrama presenta una abstracción que funciona como una superclase, que se encarga de estar abierta como extensión y mantiene cerradas las clases principales del sistema, para ello se modifico como las clases obtienen sus datos, se les implemento un método específico para actuarlizar su usuario asociado y no tienen una relación directa con la clase Usuario.

Las interface introducida es:
- "IObtenerActor", del cual dependen las clases Proyecto,Etapa y Comentario, y se extiende a la clase Usuario.
La interfaz provee el método obtenerActor() para acceder a las clases extendidas y obtener su nombre/identificador que proveera a las clases principales. Se utilizo el término Actor para abarcar una mayor reutilización  frente a las clases principales con las que se relacione y en caso de modificaciones a la clase Usuario, o extensión a otras clases.