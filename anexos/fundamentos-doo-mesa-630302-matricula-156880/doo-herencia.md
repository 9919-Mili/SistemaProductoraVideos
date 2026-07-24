# Herencia

La herencia permite modelar relaciones de generalización y especialización dentro del diseño orientado a objetos. Mediante este mecanismo, una clase base define atributos y comportamientos comunes que pueden ser reutilizados y ampliados por clases más específicas, evitando duplicar información y representando correctamente las relaciones existentes dentro del dominio del problema.

En el sistema de gestión de la productora de videos, la herencia se utiliza para representar que un **Adjunto** es un tipo particular de **Archivo**. La clase base reúne las características comunes de cualquier archivo utilizado por el sistema, mientras que la clase derivada incorpora la información específica necesaria para asociarlo a una etapa del proyecto.

Desde el punto de vista de los principios **SOLID**, la herencia se relaciona principalmente con:

- **Open/Closed Principle (OCP):** permite incorporar nuevos tipos de archivos sin modificar la clase base.
- **Liskov Substitution Principle (LSP):** cualquier objeto de la clase `Adjunto` puede utilizarse donde se espere un objeto de tipo `Archivo`.
- **Dependency Inversion Principle (DIP):** las clases pueden trabajar sobre la abstracción `Archivo` sin depender de una implementación concreta.

Asimismo, la herencia constituye un mecanismo ampliamente utilizado por distintos patrones de diseño. En este proyecto sirve como base para mantener una jerarquía clara entre los elementos del dominio y facilita futuras extensiones del sistema sin afectar el código existente.

---

## Ejemplo en el proyecto

En el sistema la herencia se representa mediante la clase abstracta **Archivo**, que concentra la información común de cualquier archivo administrado por la aplicación.

La clase **Adjunto** hereda de **Archivo**, reutilizando sus atributos generales e incorporando información específica como la dirección del recurso y su descripción. Esta relación expresa correctamente que un archivo adjunto es un tipo particular de archivo dentro del sistema.

### Fragmento del diagrama UML

![Diagrama Herencia](/diagramas/01-diagrama-clases/01-doo-herencia.png)

[Ver diagrama en detalle](/diagramas/01-diagrama-clases/01-doo-herencia.puml)

### Justificación técnica

El diagrama muestra una relación de generalización entre `Archivo` y `Adjunto`. La clase base concentra los atributos compartidos por todos los archivos, mientras que la subclase incorpora únicamente las características propias de un archivo adjunto. Este diseño evita la duplicación de información, facilita la reutilización de la estructura común y permite agregar nuevas especializaciones sin modificar la jerarquía existente.

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

Este fragmento aplica el principio de herencia porque `Adjunto` extiende la clase abstracta `Archivo`, reutilizando los atributos y comportamientos comunes definidos en la superclase. De esta manera, la clase derivada incorpora únicamente la información específica que necesita, evitando duplicar código y representando correctamente la relación "es un". Además, esta jerarquía permite incorporar nuevas especializaciones de `Archivo` en el futuro sin modificar la clase base, favoreciendo la extensibilidad y el mantenimiento del sistema.