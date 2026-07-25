# Herencia

La herencia permite establecer relaciones entre una clase general y otras más específicas. Mediante este mecanismo, una clase base define atributos y comportamientos comunes que pueden ser reutilizados por las clases derivadas, evitando duplicar información y facilitando la organización del sistema.

En el sistema de gestión de la productora de videos, la herencia se utiliza para representar que un Adjunto es un tipo particular de Archivo. La clase base reúne las características comunes de los archivos del sistema, mientras que la clase derivada incorpora la información necesaria para representar un archivo asociado a una etapa del proyecto.

Desde el punto de vista de los principios SOLID, la herencia se relaciona principalmente con:

- **Open/Closed Principle (OCP):** permite incorporar nuevos tipos de archivos sin modificar la clase base.
- **Liskov Substitution Principle (LSP):** cualquier objeto de la clase `Adjunto` puede utilizarse donde se espere un objeto de tipo `Archivo`.
- **Dependency Inversion Principle (DIP):** las clases pueden trabajar sobre la abstracción `Archivo` sin depender de una implementación concreta.

---

## Ejemplo en el proyecto

En el sistema, la herencia se representa mediante la clase abstracta Archivo, que concentra la información común de cualquier archivo administrado por la aplicación.

La clase Adjunto hereda de Archivo, reutilizando sus atributos generales e incorporando información específica, como la URL y la descripción del archivo asociado a una etapa del proyecto. Esta relación representa que un archivo adjunto es un tipo particular de archivo dentro del sistema.

### Fragmento del diagrama UML

![Diagrama Herencia](/diagramas/01-diagrama-clases/01-doo-herencia.png)

[➡ Ver diagrama completo en detalle](/diagramas/01-diagrama-clases/01-diagrama-clases-final.png)

### Justificación técnica

El diagrama muestra una relación de generalización entre Archivo y Adjunto. La clase base reúne la información común de los archivos, mientras que la subclase incorpora las características específicas de un archivo adjunto.
Este diseño evita la duplicación de información, favorece la reutilización del código y permite incorporar nuevas especializaciones sin modificar la estructura existente.

---

## Ejemplo de Código

public abstract class Archivo {

    protected String ubicacion;
    protected String nombreArchivo;

    public String obtenerNombre() {
        return nombreArchivo;
    }

    public String obtenerUbicacion() {
        return ubicacion;
    }
}

public class Adjunto extends Archivo {

    private String url;
    private String descripcion;

    public void vincularRecurso() {
        // Lógica para asociar el archivo a una etapa
    }
}

### Justificación técnica

Este fragmento aplica el principio de herencia porque Adjunto extiende la clase abstracta Archivo, reutilizando los atributos y comportamientos definidos en la superclase. De esta manera, la clase derivada incorpora únicamente la información específica que necesita, evitando duplicar código y manteniendo una relación de generalización donde Adjunto es un tipo particular de Archivo.
Esta jerarquía facilita la reutilización del código y permite incorporar nuevas especializaciones sin modificar la clase base.