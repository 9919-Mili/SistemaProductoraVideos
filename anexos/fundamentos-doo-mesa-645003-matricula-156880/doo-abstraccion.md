# Abstracción

La abstracción consiste en representar los aspectos esenciales de un objeto, ocultando los detalles de su implementación. De esta manera, las clases pueden trabajar sobre conceptos generales sin depender de cómo se implementa cada caso particular.

En el sistema de gestión de la productora de videos, este principio se aplica mediante la clase abstracta Archivo, que representa el concepto general de cualquier archivo utilizado por el sistema. Las clases que necesiten trabajar con archivos pueden hacerlo utilizando esta abstracción, independientemente del tipo específico de archivo.

Desde el punto de vista de los principios SOLID, la abstracción se relaciona principalmente con:

- **Dependency Inversion Principle (DIP):** las clases pueden depender de la abstracción **Archivo** en lugar de depender directamente de implementaciones concretas.
- **Open/Closed Principle (OCP):** es posible incorporar nuevos tipos de archivos mediante nuevas subclases sin modificar la clase base.
- **Liskov Substitution Principle (LSP):** cualquier subclase de **Archivo** puede utilizarse donde se espere un objeto de ese tipo sin alterar el comportamiento del sistema.

La utilización de una clase abstracta permite desacoplar el resto del sistema de las implementaciones concretas, facilitando la reutilización del código, la extensibilidad del modelo y el mantenimiento de la aplicación a medida que evolucionen los requisitos del proyecto.

---

## Ejemplo en el proyecto

En el proyecto, la abstracción se representa mediante la clase abstracta Archivo, que define la información común de cualquier archivo utilizado dentro del sistema, como su ubicación y nombre.

La clase Adjunto hereda de Archivo, incorporando la información necesaria para representar un archivo asociado a una etapa del proyecto. De esta forma, el sistema puede trabajar con la abstracción Archivo sin depender de una implementación concreta.

En el fragmento del diagrama también se observan las clases Etapa, Usuario, Observacion y Cliente, que forman parte del modelo del sistema y muestran cómo la abstracción Archivo se integra con el resto de los elementos que participan en la gestión de los proyectos.

En el diagrama de clases del sistema se define:

- `Archivo` como clase abstracta.
- `Adjunto` como clase concreta que hereda de `Archivo`.

---
```
Fragmento de diagrama UML

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
```

![Diagrama de Abstracción](/diagramas/01-diagrama-clases/diagrama-doo-abstraccion-156880.png)

[➡ Ver diagrama completo en detalle](/diagramas/01-diagrama-clases/01-diagrama-clases-final.png)

---

### Justificación técnica del diagrama

El diagrama muestra que Archivo es una clase abstracta que reúne las características comunes de los archivos del sistema y sirve como base para las clases derivadas. Adjunto reutiliza esa definición e incorpora la información específica necesaria para representar un archivo asociado a una etapa del proyecto.

El fragmento permite observar cómo esta abstracción se relaciona con otras clases del sistema, como Etapa, Usuario, Observacion y Cliente, integrándose en el modelo general sin perder su función como base de la jerarquía de archivos.

Este diseño favorece la reutilización del código y permite incorporar nuevos tipos de archivos sin modificar la estructura existente.

---

 Ejemplo de código

```
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
```
---

### Justificación técnica del código

El fragmento demuestra la aplicación de la abstracción porque el objeto se utiliza mediante el tipo Archivo, mientras que la implementación concreta corresponde a Adjunto. La clase abstracta define el comportamiento común y la clase derivada proporciona su implementación específica.

Este enfoque permite trabajar con una misma abstracción, facilita la incorporación de nuevas subclases y mejora la organización y el mantenimiento del sistema.