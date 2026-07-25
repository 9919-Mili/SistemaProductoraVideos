# Polimorfismo

El polimorfismo permite que distintos objetos de una misma jerarquía puedan utilizarse mediante una referencia común, ejecutando el comportamiento correspondiente a su tipo concreto. De esta manera, las clases trabajan sobre abstracciones en lugar de depender de implementaciones específicas, logrando un diseño más flexible y fácil de extender.

En el sistema de gestión de la productora de videos, el polimorfismo se aplica mediante la jerarquía formada por la clase abstracta Archivo y su subclase Adjunto. Aunque actualmente solo existe la implementación Adjunto, esta estructura permite incorporar nuevos tipos de archivos sin modificar las clases que trabajan con la abstracción Archivo.

Desde el punto de vista de los principios SOLID, el polimorfismo se relaciona principalmente con:

- **Open/Closed Principle (OCP):** permite incorporar nuevas subclases sin modificar las clases que trabajan con la abstracción.
- **Liskov Substitution Principle (LSP):** cualquier instancia de `Adjunto` puede sustituir a un objeto `Archivo` sin alterar el comportamiento esperado.
- **Dependency Inversion Principle (DIP):** las clases pueden depender de la abstracción `Archivo` en lugar de depender de implementaciones concretas.

---

## Ejemplo en el proyecto

En el proyecto, el polimorfismo se observa en la relación entre las clases Archivo y Adjunto.

La clase Archivo representa la abstracción común para los archivos del sistema, mientras que Adjunto proporciona una implementación concreta para representar los archivos asociados a las etapas de un proyecto.

Gracias a esta jerarquía, el sistema puede trabajar con objetos del tipo Archivo sin depender de una implementación específica, facilitando la incorporación de nuevas subclases en el futuro.

### Fragmento del diagrama UML

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

![Diagrama Polimorfismo](/diagramas/01-diagrama-clases/01-doo-polimorfismo.png)

[➡ Ver diagrama completo en detalle](/diagramas/01-diagrama-clases/01-diagrama-clases-final.png)

### Justificación técnica

El diagrama muestra que Adjunto hereda de Archivo, permitiendo que un objeto de la subclase pueda utilizarse mediante una referencia del tipo base. Este diseño favorece el trabajo sobre abstracciones y facilita la incorporación de nuevas especializaciones sin modificar la estructura existente.

---

## Ejemplo de Código

public abstract class Archivo {

    protected String nombreArchivo;
    protected String ubicacion;

    public abstract String obtenerUbicacion();
}

public class Adjunto extends Archivo {

    private String url;
    private String descripcion;

    public Adjunto(String nombreArchivo, String url, String descripcion) {
        this.nombreArchivo = nombreArchivo;
        this.url = url;
        this.descripcion = descripcion;
    }

    @Override
    public String obtenerUbicacion() {
        return url;
    }
}

Archivo archivo = new Adjunto(
    "video_final.mp4",
    "https://drive.com/video",
    "Versión final aprobada"
);

System.out.println(archivo.obtenerUbicacion());


### Justificación técnica

Este fragmento demuestra el principio de polimorfismo porque la variable archivo está declarada como tipo Archivo, mientras que el objeto creado es de tipo Adjunto. Al invocar el método obtenerUbicacion(), se ejecuta la implementación correspondiente a la clase concreta.
De esta manera, el sistema puede trabajar con distintos tipos de archivos mediante una misma referencia, favoreciendo la reutilización del código, el mantenimiento y la incorporación de nuevas subclases.