# Anexo – Aplicación de Patrón de Diseño Creacional –
Patron de Diseño Creacional Factory Method

## Patrones de Diseño Creacionales y su relación con SOLID

Los patrones de diseño creacionales se utilizan para crear objetos de manera flexible y reutilizable, manteniendo la independencia respecto de los tipos concretos de objetos que tengamos que crear. Dichos patrones se alinean de manera perfecta con los principios SOLID, permitiendo código más mantenible, escalable y testeable. Se relaciona con el principio SOLID OCP por que el patron de diseño elegido permite que el sistema se encuentre abierto para extensiones, pero cerrado para modificaciones. Se podria agregar nuevos tipos de notificaciones (ej: wpp, texto) creando clases especificas, sin tener que modificar el codigo que ya existe. 

## Propósito y Tipo del Patrón

### Propósito:
El patrón seleccionado es Factory Method, por que resuelve el problema de la creación de objetos enlazando al cliente a clases concretas. En el caso del sistema de Notificacion, el problema específico era que sin el patrón cada vez que quisiera crear una notificacion tendria que saber exactamente que clase solicitar. 

### Tipo 
Factory Method es el seleccionado, por que cada vez que necesitaramos crear una notificación (email, sms u otro medio), tendriamos que conocer exactamente qué clase instanciar. Si añadimos nuevos tipos de notificaciones, el código cliente deberia cambiar.
Factory Method encapsula la lógica de creación en clases especializadas, permitiendo que el código cliente solo dependa de la interfaz Notificacion, no de sus implementaciones concretas.
En el caso del sistema de notificaciones, proporciona una arquitectura escalable, mantenible y que sigue completamente los principios SOLID OCP. 
La implementación permite agregar nuevos canales de notificación sin modificar el código existente, lo cual es especialmente valioso en sistemas que evolucionan continuamente.


# Motivacion 
El sistema de notificaciones originalmente tenía una única clase Notificacion que manejaba todos los tipos de notificaciones (email, SMS). Esta implementación generaba acoplamiento y violaba el Principio de Responsabilidad Única (SRP).
La clase Notificacion tenia metodos como: enviarNotificacion(), prepararNotificacion() y enviarNotificacionResponsable(), con la condicional if-else que se basaba en el tipo de notificacion.
Por lo que generaba problemas de mantenibilidad y escalabilidad por que al agregar un nuevo tipo de notificacion se necesitaba modificar la clases existente violando el principio OCP. Cualquier tipo de cambio iba a modificar toda la clase. 
Se incoporan nuevas clases como: NotificacionInternaCreador(abstracta) con subclases SmsNotificacionCreador, EmailNotificacionCreador y NotificacionCreador. 
Factory Method engloba la lógica de creación de creadores especializados. Cada creador es responsable de solicitar su tipo específico de notificación. Lo que permite que el código que necesite de Notificacion trabaje con abstracciones, delegando la creación a las subclases. Se elimina el código condicional, se respeta SRP (cada clase tiene una responsabilidad), y se cumple OCP (abierto para extensión, cerrado para modificación).

# Estructuras de clases 

9919-Mili/SistemaProductoraVideos/diagramas/01-diagrama-clases/01-patron-creacional-factory-method.png 

# Justificación Técnica de la Estructura de Clases

- Interfaz Notificacion

Responsabilidad: Define la interfaz común que deben cumplir todas las notificaciones. Garantiza que todas implementen prepararNotificacion() y enviarNotificacion().

Relacion: Es implementada por las clases EmailNotificacion, SmsNotificacion y NotificacionInterna.

Justificación: Permite que el Creador opere sobre un tipo abstracto sin conocer la clase concreta que está utilizando. Esto habilita la variabilidad necesaria del patrón Factory Method.

- Clase EmailNotificacion

Responsabilidad: Representa un producto concreto que implementa la interfaz Notificacion. Contiene los datos y la lógica necesaria para enviar notificaciones por una determinada via. 

Relacion: Implementa Notificacion, creada por EmailNotificacionCreador.

Justificación: Ejemplifica una de las variantes del producto, necesaria para demostrar cómo el patrón crea diferentes tipos de objetos a partir del mismo Creador.

- Clase SmsNotificacion

Responsabilidad: Encapsula la lógica para notificaciones vía SMS.

Relacion: Implementa Notificacion, creada por SmsNotificacionCreador.

Justificación: Refuerza la necesidad del patrón: distintos productos que respetan una interfaz común y se crean mediante el Factory Method.

- Clase NotificacionInterna

Responsabilidad: Modela una notificación interna dentro del sistema.

Relacion: Implementa Notificacion, se instancia mediante NotificacionInternaCreador.

Justificación: Ofrece un tercer ejemplo de producto, ampliando la flexibilidad del diseño.

- Clase abstracta NotificacionCreador (Creador)

Responsabilidad: Define el factory method enviar() que orquesta la creación y el envío de cualquier tipo de notificación. Declara el método abstracto crearNotificacion().

Relacion: Es extendida por los creadores concretos. Tiene una dependencia hacia Notificacion, ya que enviar() usa el producto retornado por crearNotificacion().

Justificación: Es el elemento clave del patrón. Aíslas el algoritmo principal del proceso, permitiendo que las subclases determinen qué producto concreto se crea.

- Clases concretas EmailNotificacionCreador, SmsNotificacionCreador, NotificacionInternaCreador

Responsabilidad: Implementan el Factory Method crearNotificacion() y deciden qué tipo de notificación crear.

Relacion: Extienden NotificacionCreador. Producen instancias de las clases concretas que implementan Notificacion.

Justificación: Permiten variar el tipo de producto sin modificar la lógica general definida en enviar(), cumpliendo así con el Principio SOLID OCP. 

- Explicación 

El flujo inicia cuando el cliente solicita enviar() sobre una instancia del creador concreto. enviar() actúa como Template Method, llamando al Factory Method crearNotificacion(), sin conocer la clase concreta que se va a instanciar. Por lo que obtiene un objeto del tipo abstracto Notificacion.
El Creador depende de la interfaz Notificacion, por lo que puede ejecutar: prepararNotificacion() o enviarNotificacion().
La creación concreta del objeto (instanciación) se delega a las subclases del creador:
EmailNotificacionCreador crea un EmailNotificacion
SmsNotificacionCreador crea un SmsNotificacion
NotificacionInternaCreador crea un NotificacionInterna. 
Por lo que enviar() completa el algoritmo y entrega el comportamiento final al cliente sin que éste conozca los detalles de qué clase concreta se utilizo. 


Esta estructura permite extender nuevos tipos de notificación sin modificar el creador, encapsular la lógica de creación de objetos, mantener un algoritmo común desacoplado del producto específico y cumplir los principios SOLID. 