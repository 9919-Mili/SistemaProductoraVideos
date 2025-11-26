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
Se incoporan nuevas clases como: NotificacionInternaCreador(abstracta) con subclases SmsNotificacionCreador, EmailNotificacionCreador y NotificacionCreador 
Factory Method engloba la lógica de creación de creadores especializados. Cada creador es responsable de solicitar su tipo específico de notificación. Lo que permite que el código que necesite de Notificacion trabaje con abstracciones, delegando la creación a las subclases. Se elimina el código condicional, se respeta SRP (cada clase tiene una responsabilidad), y se cumple OCP (abierto para extensión, cerrado para modificación).

# Estructuras de clases 

# Justificación Técnica de la Estructura de Clases

● Descripción detallada de cada clase incluida en el diagrama, indicando:

● Explicación del flujo de creación de objetos: