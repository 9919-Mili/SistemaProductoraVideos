## Abstracción

La abstracción en el diseño orientado a objetos consiste en modelar conceptos relevantes mediante clases o interfaces que representan su comportamiento esencial, ocultando los detalles de implementación.

Este principio permite que los objetos interactúen a través de contratos bien definidos, sin necesidad de conocer cómo están implementados internamente. El sistema expone únicamente las operaciones necesarias para su uso, manteniendo encapsulada la lógica interna.

En el sistema de gestión de la productora de videos, la abstracción se aplica mediante la clase abstracta **Archivo**, que representa el concepto general de cualquier archivo asociado al proyecto sin definir una implementación concreta. Las clases que necesiten trabajar con archivos pueden hacerlo utilizando esta abstracción, independientemente del tipo específico de archivo que se utilice.

Desde el punto de vista de los principios **SOLID**, este fundamento se relaciona principalmente con:

- **Dependency Inversion Principle (DIP):** las clases pueden depender de la abstracción **Archivo** en lugar de depender directamente de implementaciones concretas.
- **Open/Closed Principle (OCP):** es posible incorporar nuevos tipos de archivos mediante nuevas subclases sin modificar la clase base.
- **Liskov Substitution Principle (LSP):** cualquier subclase de **Archivo** puede utilizarse donde se espere un objeto de ese tipo sin alterar el comportamiento del sistema.

La abstracción también constituye la base de numerosos patrones de diseño orientados a objetos. En este proyecto se encuentra presente tanto en el patrón creacional **Factory Method**, donde el sistema trabaja sobre la abstracción `Notificacion`, como en el patrón de comportamiento **Observer**, que desacopla emisores y receptores mediante las interfaces `Subject` y `Observer`. Gracias a estas abstracciones, el sistema puede extenderse incorporando nuevas implementaciones sin modificar el código existente.


---

### Ejemplo en el proyecto

En el proyecto, la abstracción se representa mediante la clase abstracta **Archivo**, que define la información común de cualquier archivo utilizado dentro del sistema, como su ubicación y nombre.

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

![Diagrama de Abstracción](/diagramas/01-diagrama-clases/diagrama-doo-abstraccion.png)

[Ver diagrama en detalle](/diagramas/01-diagrama-clases/diagrama-doo-abstraccion.png)

---

# Justificación técnica del diagrama

La clase abstracta **Archivo** representa el concepto general de cualquier archivo utilizado dentro del sistema, definiendo únicamente la información y el comportamiento común que compartirán todas sus implementaciones. Al ser una clase abstracta, no puede instanciarse directamente, sino que sirve como base para las clases concretas.

La clase **Adjunto** reutiliza esa definición general mediante herencia e incorpora los atributos específicos necesarios para representar un archivo asociado a una etapa del proyecto.

Esta estructura permite que otras clases trabajen con la abstracción **Archivo** sin depender de implementaciones concretas. Si en el futuro fuera necesario incorporar nuevos tipos de archivos, bastaría con crear nuevas subclases de **Archivo**, manteniendo el resto del sistema sin modificaciones y favoreciendo un diseño flexible, reutilizable y alineado con los principios SOLID.

---

# Ejemplo de código

abstract class Archivo {

    protected String ubicacion;
    protected String nombreArchivo;

    public abstract void abrir();
}

class Adjunto extends Archivo {

    private String url;
    private String descripcion;

    @Override
    public void abrir() {
        System.out.println("Abriendo archivo: " + nombreArchivo);
    }
}

Archivo archivo = new Adjunto();
archivo.abrir();

---

# Justificación técnica del código

El fragmento demuestra la aplicación de la abstracción porque el objeto se utiliza mediante el tipo abstracto **Archivo**, sin que el código cliente dependa directamente de la implementación concreta **Adjunto**. La clase abstracta define las características comunes y el comportamiento que deberán implementar todas las clases derivadas, mientras que **Adjunto** proporciona la implementación específica del método `abrir()`.

Gracias a este enfoque, el sistema puede trabajar con cualquier tipo de archivo utilizando la misma abstracción, ocultando los detalles internos de implementación y facilitando la incorporación de nuevos tipos de archivos sin modificar el código existente. Esto reduce el acoplamiento entre componentes, favorece la reutilización del código y mejora la mantenibilidad del sistema.