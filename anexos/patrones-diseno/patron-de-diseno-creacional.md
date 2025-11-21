# Anexo – Aplicación de Patrón de Diseño Creacional –
Patron de Diseño Creacional Factory Method

##Patrones de Diseño Creacionales y su relación con SOLID
Los patrones de diseño creacionales se utilizan para crear objetos de manera flexible y reutilizable, manteniendo la independencia respecto de los tipos concretos de objetos que tengamos que crear. Dichos patrones se alinean de manera perfecta con los principios SOLID, permitiendo código más mantenible, escalable y testeable.

## Propósito y Tipo del Patrón

### Propósito:
El patrón Factory Method resuelve el problema de la creación de objetos enlazando al cliente a clases concretas. En el caso del sistema de Notificacion, el problema específico era que sin el patrón 

### Tipo 
Factory Method, cada vez que necesitaramos crear una notificación (email, sms u otro medio), tendriamos que conocer exactamente qué clase instanciar. Si añadimos nuevos tipos de notificaciones, el código cliente deberia cambiar.
Factory Method encapsula la lógica de creación en clases especializadas, permitiendo que el código cliente solo dependa de la interfaz Notificacion, no de sus implementaciones concretas.
En el caso del sistema de notificaciones, proporciona una arquitectura escalable, mantenible y que sigue completamente los principios SOLID.
La implementación permite agregar nuevos canales de notificación sin modificar el código existente, lo cual es especialmente valioso en sistemas que evolucionan continuamente.


# Motivacion 


# Estructuras de clases 

# Justificación Técnica de la Estructura de Clases

● Descripción detallada de cada clase incluida en el diagrama, indicando:

● Explicación del flujo de creación de objetos: