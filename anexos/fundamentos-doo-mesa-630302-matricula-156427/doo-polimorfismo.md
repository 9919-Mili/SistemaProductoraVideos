# Polimorfismo

El polimorfismo consiste en la capacidad de los objetos de diferentes clases relacionadas por herencia o por interfaces de responder al mismo método de distintas formas. Esto permite que un mismo método pueda ser invocado sobre diferentes tipos de objetos, y cada uno responderá según su propia implementación, facilitando la flexibilidad y extensibilidad del sistema.

El polimorfismo está estrechamente ligado a varios principios SOLID, ya que promueve la responsabilidad única **(SRP)** al permitir que cada clase implemente solo el comportamiento que le corresponde y especializar las caracteristicas heredadas, y el principio abierto/cerrado **(OCP)** al posibilitar la extensión de funcionalidades mediante nuevas implementaciones sin modificar el código existente. Además, el polimorfismo es clave para la segregación de interfaces **(ISP)**, ya que permite definir interfaces específicas para distintos comportamientos.

El polimorfismo es fundamental en muchos patrones de diseño. Patrones creacionales como **Factory Method** y **Abstract Factory** lo utilizan para crear objetos de diferentes tipos a través de una interfaz común. Patrones estructurales como **Adapter** y **Decorator** aprovechan el polimorfismo para modificar o extender el comportamiento de los objetos sin cambiar su código. Patrones de comportamiento como **Strategy**, **State** y **Observer** dependen del polimorfismo para permitir que los objetos cambien su comportamiento en tiempo de ejecución o respondan de manera flexible a eventos y mensajes.

## Ejemplo en el proyecto

Esta parte del diagrama refleja el polimorfismo de una clase del Sistema Productora de Vídeos:

![Diagrama de Clases Final](/diagramas/01-diagrama-clases/diagrama-doo-polimorfismo-156427.png)

[➡ Ver diagrama completo en detalle](/diagramas/01-diagrama-clases/01-diagrama-clases-final.puml)


**Clases `Archivo` y `Adjunto`**

Gracias a su estructura simple, cualquier objeto que herede de `Archivo` puede ser tratado de manera uniforme por otras clases del sistema, como `Etapa`, que puede manipular listas de archivos de la clase `Adjunto` sin importar su tipo concreto.

**Atributos heredados modificados:** `ubicación` recibio una modificación para adaptarse al entorno de la nube como `url`.  
**Relaciones:** la clase `Etapa` utiliza una lista de Adjuntos a partir de su `nombre` y `url`.

**Justificación técnica:** Al heredar el concepto de "ubicacion" en su clase derivada, se logra polimorfismo que permite que `Adjunto` trabaje con el atributo de `Archivo` sin depender de seguir su mismo formato, pues adapta el atributo ubicación a url para utilizarlo en el sistema, esto permite que clases trabajen con cualquier objeto que sea una instancia de Archivo, cosa que podria implementarse con una mayor variedad como la lista de Adjuntos en la clase de Etapa, aprovechando el polimorfismo para invocar métodos que pueden tener implementaciones distintas según el tipo real del objeto. Así, se facilita la extensión del sistema (OCP), y las clases dependen de abstracciones y no de implementaciones concretas (DIP).

## Ejemplo de Código

```
abstract class Archivo {
    - ubicacion: string
    - nombreArchivo: string
}

class Adjunto {
    - url: string
    - descripcion: string
    - nombreArchivo: string
    + vincularRecurso(url: string, descripcion: string, nombreArchivo: string): Adjunto
}
```
Este fragmento de código cumple el fundamento de polimorfismo porque define una clase abstracta `Archivo` y una clase concreta `Adjunto` que la extiende. Así, cualquier objeto de tipo `Adjunto` puede ser tratado como un `Archivo` por otras clases, permitiendo que métodos y atributos definidos en la abstracción sean utilizados de manera uniforme, aunque cada subclase pueda implementar o especializar su propio comportamiento. 