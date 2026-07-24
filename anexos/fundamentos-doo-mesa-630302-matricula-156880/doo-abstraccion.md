## Abstracción

La abstracción en el diseño orientado a objetos consiste en modelar conceptos relevantes mediante clases o interfaces que representan su comportamiento esencial, ocultando los detalles de implementación.

Este principio permite que los objetos interactúen a través de contratos bien definidos, sin necesidad de conocer cómo están implementados internamente. El sistema expone únicamente las operaciones necesarias para su uso, manteniendo encapsulada la lógica interna.

En el sistema de gestión de la productora de videos, la abstracción se aplica mediante las interfaces **Subject** y **Observer**, que definen el comportamiento general de notificación de eventos sin especificar cómo se implementa dicha notificación.

Desde el punto de vista de **SOLID**, este fundamento se relaciona principalmente con:

- **Dependency Inversion Principle (DIP):** las clases pueden depender de la abstracción **Archivo** en lugar de depender directamente de implementaciones concretas.  
- **Liskov Substitution Principle (LSP):** es posible incorporar nuevos tipos de archivos mediante nuevas subclases sin modificar la clase base.  
- **Open/Closed Principle (OCP):** cualquier subclase de **Archivo** puede utilizarse donde se espere un objeto de ese tipo sin alterar el comportamiento del sistema.  

La abstracción también constituye la base de numerosos patrones de diseño orientados a objetos, ya que permite desacoplar el código cliente de las implementaciones concretas y trabajar sobre contratos generales.

---

### Ejemplo en el proyecto

En el proyecto la abstracción se representa mediante la clase abstracta **Archivo**, que define la información común de cualquier archivo utilizado dentro del sistema, como su ubicación y nombre.

La clase **Adjunto** hereda de **Archivo**, incorporando los atributos y comportamientos específicos necesarios para representar un archivo asociado a una etapa del proyecto. De esta forma, el resto del sistema puede trabajar con la abstracción **Archivo** sin depender de la implementación concreta de **Adjunto**.

En el diagrama de clases del sistema se define:


- `Archivo` como clase abstracta.
- `Adjunto` como clase concreta que hereda de `Archivo`.

---

### Fragmento de diagrama UML

```plantuml
@startuml

abstract class Archivo {
    - ubicacion: string
    - nombreArchivo: string
}

class Adjunto {
    - url: string
    - descripcion: string
    - nombreArchivo: string
}

Archivo <|-- Adjunto

@enduml
