# Herencia

La herencia consiste en definir nuevas clases a partir de clases existentes, permitiendo que las subclases hereden atributos y métodos de una superclase. Esto facilita la reutilización de código, la extensión de funcionalidades y la creación de jerarquías lógicas que reflejan relaciones del mundo real, permitiendo que los objetos compartan comportamientos comunes y especialicen solo lo necesario.

La herencia está estrechamente ligada a varios principios SOLID, tal como, al permitir que cada clase se enfoque en una función específica **(OCP)** y posibilitar la extensión de comportamientos mediante subclases sin modificar las clases base, y **(LSP)**, y puede facilitar la inversión de dependencias **(DIP)** al trabajar con abstracciones en las jerarquía que haya extendido algun componente de la clase base.

La herencia es fundamental en muchos patrones de diseño. Patrones creacionales como **Prototype** y **Builder** aprovechan la herencia para definir estructuras base y variantes. Patrones estructurales como **Decorator** y **Composite** utilizan la herencia para extender o combinar comportamientos. Patrones de comportamiento como **Template Method** y **Chain of Responsibility** dependen de la herencia para definir pasos de algoritmos o cadenas de procesamiento que pueden ser especializadas por las subclases.

## Ejemplo en el proyecto

Incluir un diagrama UML que muestra cómo la clase o las clases del proyecto se
relacionan entre sí al aplicar abstracción. Incluir una imagen incrustada, así como el
enlace correctamente referenciado para ver el diagrama en detalle. Describe cómo
el diagrama de las clases seleccionadas refleja la herencia. Incluir justificación técnica de cómo esas clases seleccionadas del proyecto cumplen el fundamento.


**Clase `Archivo` y `Adjunto`.**

`Adjunto` hereda de `Archivo`, lo que significa que adquiere sus atributos y comportamientos básicos, pero puede especializar o extender su funcionalidad según las necesidades del sistema.

**Atributos heredados:** `nombre` y `ubicación`, el segundo recibio una especialización a `url`. 
**Jerarquía:** `Archivo` define los atributos generales para cualquier tipo de archivo en el sistema.
`Adjunto` extiende a `Archivo`, añadiendo o especializando atributos como la descripción y comportamientos específicos para archivos adjuntos en el contexto de proyectos audiovisuales.

**Justificación técnica:** Esta estructura permite reutilizar el código común en la clase base `Archivo` y evitar duplicidad en las subclases. Si en el futuro se requieren otros tipos de archivos (por ejemplo, ArchivoTemporal o ArchivoExterno), pueden crearse nuevas subclases que hereden de Archivo sin modificar la clase base, cumpliendo así con el principio abierto/cerrado (OCP). Además, la herencia asegura que cualquier instancia de Adjunto pueda ser tratada como un Archivo, respetando el principio de sustitución de Liskov (LSP).

## Ejemplo de Código

Incluir un fragmento de código que demuestre la implementación de herencia en el
proyecto (puede ser pseudocódigo o un lenguaje como C#, JavaScript, Python o
Java, etc.). Incluir justificación técnica de cómo este fragmento de código
cumple el fundamento

```
class Adjunto {
    - url: string
    - descripcion: string
    - nombreArchivo: string
    + vincularRecurso(url: string, descripcion: string, nombreArchivo: string): Adjunto
}

abstract class Archivo {
    - ubicacion: string
    - nombreArchivo: string
}

Herencia / Especialización
Archivo <|-- Adjunto
```
Este fragmento de código cumple el fundamento de herencia al mostrar cómo la clase Adjunto hereda de la clase abstracta Archivo. De este modo, Adjunto reutiliza los atributos y comportamientos definidos en Archivo (como nombreArchivo y ubicacion), y puede especializar o agregar nuevos atributos y métodos propios, como url, descripcion y vincularRecurso. Esto evita la duplicidad de código, facilita la extensión del sistema y permite tratar a los objetos Adjunto como instancias de Archivo, cumpliendo con los principios de reutilización, extensión (OCP) y sustitución de Liskov (LSP) en el diseño orientado a objetos.