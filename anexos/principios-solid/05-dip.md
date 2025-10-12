# Principio de Inversión de Dependencias (DIP)

## Proposito y Tipo del Principio Solid

Dentro del boceto de clases, se puede ver que multiples clases dependen de otras de nivel inferior para ejecutar sus métodos, como la relacion de clase Etapa -> clase Usuario.   

Para solucionarlo se aplicara el Principio DIP para crear abstracciones de las clases que actuen como un intermediario/interfaz generalizado que eviten la dependencia de clases especificas y pueda utilizarse para reclicar codigo cuando se añadan otras clases de proposito similar, como lo son las clases Adjunto y Comentario.

## Motivación

El boceto actual contiene la clase Etapa, que depende de las clases Usuario, Adjunto y Comentario para actualizar los atributos de la clase, por lo cual esta completamente acoplada al buscar extraer información de tres clases concretas diferentes directamente.

Se usara el Principio DIP para crear abstracciones encargadas de obtener la información de los atributos de clase para reemplazar las dependencias de para actualizar/reemplazar los atributos de la clase Etapa.

## Explicación de Clases Abstractas e Interfaces

Una clase abstracta es una clase que no puede ser instanciada directamente y puede contener métodos con o sin implementación, que sirvan como base para otras clases. Mientras que las interfaces son "contratos" de métodos a implementar en las clases.

Su utilizacion en DIP, se basa en actuar como un intermediario entre clases, esto es posible al crear una abstracción que al aplicarla se reemplaza la relación directa entre clases de diferente nivel con un punto medio en que clases de alto nivel dependen de la abstracción que se implementa en las clases de bajo nivel, así se mantiene un bajo acoplamiento dentro de las clases concretas y facilita la modificar las implementaciones de diferentes clases al sistema.

## Estructura de Clases
- [Diagrama_Principio_DIP](/diagramas/01-diagrama-clases/01-solid-05-dip.png)

![Diagrama_UML_Principio](/diagramas/01-diagrama-clases/01-solid-05-dip.png)

## Justificación Técnica

El diagrama presenta una nueva manera de crear objetos y modificar los atributos de clases sin necesidad de depender de otras clases concretas de un nivel inferior, para ello se les implementaron métodos a partir de interfaces.

Las interfaces introducidas son:
- "IExtractorNombre", del cual dependen las clases Etapa y Comentario, y se extiende a la clase Usuario.
La interfaz provee el método obtenerNombre() para acceder al atributo "nombre" de la clase Usuario y responder a los métodos "actualizarResponsable()" y "actualizarAutor()" de las clases dependientes.

- "IAgregarObjeto", del cual depende la clase Etapa, y se extiende a la clases Comentario y Adjunto.   
La interfaz provee el método agregarObjeto() para crear un objeto correspondiente de las clases Comentario o Adjunto, el cual pasara directamente a formar parte de la lista del atributo "comentarios y adjuntos" de la clase Etapa.