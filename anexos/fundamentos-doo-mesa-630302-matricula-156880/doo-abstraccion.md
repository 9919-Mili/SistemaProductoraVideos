## Abstracción

La abstracción en el diseño orientado a objetos consiste en modelar conceptos relevantes mediante clases o interfaces que representan su comportamiento esencial, ocultando los detalles de implementación.

Este principio permite que los objetos interactúen a través de contratos bien definidos, sin necesidad de conocer cómo están implementados internamente. El sistema expone únicamente las operaciones necesarias para su uso, manteniendo encapsulada la lógica interna.

En el sistema de gestión de la productora de videos, la abstracción se aplica mediante las interfaces **Subject** y **Observer**, que definen el comportamiento general de notificación de eventos sin especificar cómo se implementa dicha notificación.

Desde el punto de vista de **SOLID**, este fundamento se relaciona principalmente con:

- **Dependency Inversion Principle (DIP):** las clases del dominio dependen de interfaces (Observer) y no de implementaciones concretas.  
- **Liskov Substitution Principle (LSP):** cualquier clase que implemente Observer puede sustituirse sin alterar el funcionamiento del sistema.  
- **Open/Closed Principle (OCP):** permite agregar nuevos observadores sin modificar las clases existentes.  

La abstracción es además un elemento central del patrón de comportamiento **Observer**, que desacopla emisores y receptores de eventos mediante contratos abstractos.

---

### Ejemplo en el proyecto

En el proyecto, la abstracción se implementa a través de las interfaces **Subject** y **Observer**:  
La clase **Etapa** actúa como sujeto que notifica cambios, mientras que clases como **ServicioNotificaciones**, **ResponsableDelProyecto** o **DashboardAdministrador** implementan la interfaz Observer.

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
