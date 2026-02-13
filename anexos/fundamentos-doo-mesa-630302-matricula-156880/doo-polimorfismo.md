# Polimorfismo

El polimorfismo permite que distintos objetos relacionados por una jerarquía puedan ser tratados de manera uniforme a través de una misma referencia abstracta, mientras cada uno mantiene su comportamiento específico.

En este proyecto, el polimorfismo surge a partir de la jerarquía `Archivo` → `Adjunto`. Gracias a esta relación, el sistema puede trabajar con archivos de manera general sin depender del tipo concreto que se esté utilizando.

---

## Aplicación en el Modelo

La clase `Archivo` define una abstracción común para cualquier recurso almacenado en el sistema. Al ser abstracta, establece una base compartida para sus subclases.

`Adjunto` extiende a `Archivo`, especializando su comportamiento y adaptando ciertos atributos al contexto del sistema (por ejemplo, utilizando `url` como forma concreta de ubicación).

Esto permite que otras clases, como `Etapa`, puedan manejar colecciones de tipo `Archivo` sin necesidad de conocer si el objeto concreto es un `Adjunto` u otro tipo derivado.

Ejemplo conceptual de uso:

List<Archivo> archivos;

La clase que utiliza esa lista no necesita conocer el tipo específico del archivo; simplemente opera sobre la abstracción.

---

## Manifestación del Polimorfismo

El polimorfismo se manifiesta cuando:

- Una clase trabaja con referencias del tipo `Archivo`.
- En tiempo de ejecución, el objeto real es un `Adjunto`.
- Se invocan métodos definidos en la clase base pero ejecutados según la implementación concreta.

De esta forma, se desacopla el uso del objeto de su implementación específica, permitiendo mayor flexibilidad en el diseño.

---

## Beneficios en el Sistema

1. **Flexibilidad:**  
   Se pueden incorporar nuevos tipos de archivo sin modificar las clases que ya trabajan con `Archivo`.

2. **Extensibilidad:**  
   Si se agrega una nueva subclase (por ejemplo, `ArchivoTemporal`), el sistema puede integrarla automáticamente donde se utilice la abstracción.

3. **Menor acoplamiento:**  
   Las clases dependen de la abstracción (`Archivo`) y no de implementaciones concretas (`Adjunto`).

4. **Cumplimiento de principios de diseño:**  
   Se favorece el principio abierto/cerrado (OCP) y el principio de sustitución de Liskov (LSP), ya que las nuevas implementaciones no requieren modificar código existente y pueden reemplazar correctamente a la clase base.

---

## Ejemplo de Código Representativo

```java
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

    public void vincularRecurso() {
        // lógica específica para adjuntos
    }
}
Archivo archivo = new Adjunto(
    "video_final.mp4",
    "https://drive.com/video",
    "Versión final aprobada"
);

System.out.println(archivo.obtenerUbicacion()); 
 
---

## Conclusión

El polimorfismo en el sistema se implementa mediante la utilización de la clase abstracta `Archivo` y su especialización en `Adjunto`. Esta estructura permite que el sistema trabaje con archivos de forma genérica, sin depender de implementaciones concretas.

Gracias a este enfoque, el modelo mantiene coherencia conceptual, reduce el acoplamiento entre clases y facilita la incorporación de nuevas especializaciones sin modificar el código existente. De esta manera, el polimorfismo contribuye a la flexibilidad, escalabilidad y mantenibilidad del sistema.
