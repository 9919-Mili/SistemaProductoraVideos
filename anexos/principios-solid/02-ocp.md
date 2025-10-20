# Principio Abierto/Cerrado (OCP)

## Proposito y Tipo del Principio Solid

Dentro del boceto de clases, se puede ver que varias clases estan abiertas a modificación al poseer atributos asociados directamente a una clase concreta, asi como hay partes de clases que estan acopladas y se pueden abstraer mediante extensiones a subclases.

Para solucionarlo se aplicara el Principio OCP para crear una clase abstracta con extensiones que puedan modificarse, en lugar de modificar las clases principales a partir de cada cambio necesario.

## Motivación

El boceto actual contiene la clase Notificación, que ante cualquier modificación tambien se necesitara modificar la clase Sistema, que posee un método directamente dependiente de la clase Notificación, por lo tanto esta abierta a modificación.

Se usara el Principio OCP para que la clase Notificación funcione como una clase abstracta para que las subclases extendidas notifiquen a los destinatarios de diferentes servicios.

## Explicación de Herencia

Una relación de herencia en el diseño orientado a objetos es un vínculo entre una clase base (superclase) y una clase derivada (subclase), donde la subclase hereda atributos y métodos de la superclase. Esto permite reutilizar código y extender las funcionalidades de la superclase.

Su aplicación a OCP, se da en como la herencia permite que una clase esté abierta para extensión (crear nuevas subclases con comportamientos adicionales o modificados) pero cerrada para modificación (no es necesario cambiar el código de la clase base). Así la clases Proyecto, Etapa y Tarea dependeran de una clase abstracta, de esta manera se "aislaran" las modificaciones de esas clases principales y solo se modificaran la clase Notificacion y sus extensiones.

## Estructura de Clases

- [Diagrama_Principio_OCP](/diagramas/01-diagrama-clases/01-solid-02-ocp.png)

![Diagrama_UML_Principio](/diagramas/01-diagrama-clases/01-solid-02-ocp.png)

## Justificación Técnica

El diagrama presenta una clase asbtracta que se encarga de estar abierta como extensión y mantiene cerradas las clases principales del sistema, para ello se reubico el método "notificarUsuarios()" de la clase Sistema del que se envían las Notifiaciones, y se otorgo a las clases Proyecto, Etapa y Tarea de las que pueden surgir notificaciones a los contactos respectivos del usuario correspondiente.

Las clase que se uso para modelar una abstracta es "Notificacion", de la cual dependen las clases Proyecto, Etapa y Tarea, y se extiende a la clases NotificacionEmail y NotificacionWhatsApp.
Se proveen los tres atributos requeridos para gestionar el envio de la notificación, y los métodos "detectarContacto()", para que detectar si en la lista de contactos del usuario se encuentra uno que puede enviarse a través del tipo de notificación correspondiente, y "notificarContacto" para enviar la notificación.

- Se le agregaron atributos y métodos en la clase Usuario para que posea la información de contacto necesaria para las notificaciones

- Se introdujo la clase Tarea para cumplir con el requisito funcional 2 que especifica que tanto los cambios en etapas como tareas de un proyecto deben recibir notificaciones.
