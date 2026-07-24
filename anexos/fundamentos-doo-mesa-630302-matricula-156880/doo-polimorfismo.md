# Polimorfismo

El polimorfismo permite que distintos objetos relacionados por una misma jerarquía puedan ser utilizados mediante una referencia común, ejecutando el comportamiento correspondiente a su tipo concreto. Gracias a este principio, las clases trabajan sobre abstracciones en lugar de depender de implementaciones específicas, logrando un sistema más flexible y extensible.

En el sistema de gestión de la productora de videos, el polimorfismo se aplica mediante la jerarquía formada por la clase abstracta **Archivo** y su subclase **Adjunto**. Aunque actualmente solo existe una implementación concreta, cualquier objeto de tipo `Adjunto` puede utilizarse donde el sistema espere un objeto de tipo `Archivo`, permitiendo incorporar nuevos tipos de archivos sin modificar el código existente.

Desde el punto de vista de los principios **SOLID**, el polimorfismo se relaciona principalmente con:

- **Open/Closed Principle (OCP):** permite incorporar nuevas subclases sin modificar las clases que trabajan con la abstracción.
- **Liskov Substitution Principle (LSP):** cualquier instancia de `Adjunto` puede sustituir a un objeto `Archivo` sin alterar el comportamiento esperado.
- **Dependency Inversion Principle (DIP):** las clases pueden depender de la abstracción `Archivo` en lugar de depender de implementaciones concretas.

Asimismo, el polimorfismo es utilizado por diversos patrones de diseño. En **Factory Method**, distintos objetos pueden crearse mediante una misma interfaz; en **Observer**, diferentes observadores responden al mismo contrato; y en **Composite**, componentes simples y compuestos pueden tratarse de forma uniforme.

---

## Ejemplo en el proyecto

En el proyecto, el polimorfismo se observa en la relación entre las clases **Archivo** y **Adjunto**.

La clase **Archivo** representa la abstracción común para cualquier archivo utilizado por el sistema, mientras que **Adjunto** constituye una implementación concreta destinada a asociar recursos a las etapas de un proyecto.

Gracias a esta jerarquía, otras clases pueden trabajar con objetos del tipo `Archivo` sin depender de si el objeto concreto es un `Adjunto` u otra especialización que pudiera incorporarse en el futuro.

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

[Ver diagrama en detalle](/diagramas/01-diagrama-clases/01-doo-polimorfismo.puml)

### Justificación técnica

El fragmento seleccionado muestra que **Adjunto** hereda de **Archivo**, permitiendo que cualquier objeto de la subclase sea tratado mediante una referencia de la clase base. De esta forma, el sistema trabaja sobre la abstracción y no sobre implementaciones concretas, reduciendo el acoplamiento y facilitando la incorporación de nuevas especializaciones sin modificar el código existente.

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
```

### Justificación técnica

Este fragmento demuestra el polimorfismo porque la variable `archivo` está declarada como tipo `Archivo`, pero en tiempo de ejecución contiene un objeto de tipo `Adjunto`. Al invocar el método `obtenerUbicacion()`, se ejecuta la implementación correspondiente a la clase concreta. Esto permite que el sistema manipule objetos mediante la abstracción `Archivo`, facilitando la reutilización del código, el mantenimiento y la incorporación de nuevas subclases sin afectar a las clases que ya utilizan esta jerarquía.