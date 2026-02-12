# Abstracción

La abstracción consiste en identificar y modelar las características esenciales de un objeto, ignorando los detalles irrelevantes para representar entidades del mundo real mediante clases u objetos, enfocándose solo en los atributos y comportamientos necesarios para que diferentes equipos trabajen con interfaces claras y bien definidas sin necesidad de conocer la implementación interna.

La abstracción está estrechamente ligada a varios principios SOLID, pues al abstraer una clase queda definida en la misma solo las responsabilidad necesarias que deben ser unicas (SRP), cerradas que se necesiten modificaciones, sino en su lugar se extienda (OCP) a a depender de una o varias interfaces con los metodos/funciones necesarios definidos (ISP), asi reemplazando cualquier posible dependencia de una clase concreta.

La abstracción es la piedra angular de muchos patrones de diseño. Los patrones creacionales como **Factory Method** y **Abstract Factory** utilizan abstracción para desacoplar la creación de objetos de su uso. Los patrones estructurales como **Adapter** y **Facade** aprovechan la abstracción para simplificar interfaces complejas. Los patrones de comportamiento como **Strategy** y **Observer** dependen de abstracciones para permitir cambios dinámicos de comportamiento en tiempo de ejecución.

## Ejemplo en el proyecto

### Diagrama de Clases Final

El diagrama refleja la abstracción en múltiples clases que relacionadas del Sistema Productora de Vídeos:

![Diagrama de Clases Final](/diagramas/01-diagrama-clases/diagrama-doo-abstraccion.png)

[➡ Ver diagrama completo en detalle](/diagramas/01-diagrama-clases/01-diagrama-clases-final.puml)

**Clase `Etapa`**

`Etapa` abstrae una parte del proyecto mostrando solo comportamientos esenciales correspondientes a su estado y elementos:

- **Métodos principales**: `actualizarEstado()`, `agregarObservaciones()`, `registrarAdjuntos()`.
- **Relaciones**: Tiene atributos que se componen de `Observacion` y `Adjunto`, y se relaciona con un `Usuario` como responsable.
- **Responsabilidades bien definidas**: Gestiona cambios de estado y recopila elementos asociados al proyecto, sin preocuparse por notificaciones, almacenamiento o análisis.

**Justificación técnica:** La abstracción de `Etapa` permite que el sistema sea extensible. Si en el futuro se necesitan nuevos tipos de etapa o comportamientos especializados, se pueden crear subclases de `Etapa` sin afectar el código existente (OCP). Las relaciones con `Observacion` y `Adjunto` abstraen el contenido de la etapa sin exponer sus detalles.

---
**Clases `Observacion` y `Usuario`**

`Observacion` abstrae los comentarios, notas y feedback en el proyecto y se relaciona con `Usuario`:

- **Atributos simples**: `texto`, `fecha`, `autor`.
- **Método esencial**: `agregarObservacion()`, `actualizarAutor()`.
- **Relación con `Usuario`**: A través de la referencia `autor : Usuario`, abstre quién hizo la observación sin detalles de su perfil.

**Justificación técnica:** La abstracción tras separar `Observacion` de `Etapa` cumple con SRP. `Observacion` solo gestiona observaciones, mientras que `Etapa` gestiona etapas. Esto facilita que observaciones se reutilicen en otros contextos sin acoplamiento.

---
**Clase Abstracta `Adjunto` y `Archivo`**

La clase `Adjunto` es una abstraccion de un elemento cargado a la nube accesible desde el proyecto, mientras que `Archivo` es una abstracción de los diferentes tipos de archivos que pueden formar parte deñ proyecto. 

- **Atributos esenciales**: Solo exponen `ubicacion`/`url` y `nombreArchivo` (y `descripción` en caso del adjunto),  ignorando detalles como codificación, resolución o formato.
- **Encapsulamiento de detalles**: El sistema no necesita saber cómo se gestiona internamente cada tipo específico de archivo adjunto, permitiendo futuros tipos sin cambios en las clases que las utilizan.

**Justificación técnica:** Al abstraer el concepto de "archivo" y "adjunto" en una clase base, se logra que el sistema trabaje con cualquier tipo de `Archivo` sin depender de implementaciones específicas. Esto cumple con el Principio de Inversión de Dependencias (DIP), donde `Adjunto` depende de la abstracción `Archivo` en lugar de clases concretas.


## Ejemplo de Código

 Incluir justificación técnica de cómo este fragmento de código cumple el fundamento de asbtraccion.

```
class Observacion {  
    - texto: string  
    - fecha: Date  
    - autor: Usuario  
    + crearObservacion(nombreEtapaContenedora: string, nombreObservacion: string, nombreUsuario: Usuario, texto: string): Observacion  
    + actualizarObservacion(nombreEtapaContenedora: string, nombreObservacion: string, texto: string): bool  
    + editarObservacion(texto: string): Observacion  
}
```
Este fragmento de código demuestra el principio al definir únicamente los atributos y métodos esenciales para representar la clase. Se omiten detalles como ubicación, longitud o limite de texto. Esto facilita la reutilización, el mantenimiento y la extensión de la clase, sino que solo expone los comportamientos relevantes (crear, actualizar y editar observaciones) y su interacción con aquello que modifican, alineándose con el principio de responsabilidad única (SRP).
```
abstract class Archivo {  
    - ubicacion: string  
    - nombreArchivo: string  
}
```
Este fragmento de código demuestra el principio al definir unicamente lo indispensable  de esta clase abstracta, pues su proposito es tan solo representar cualquier tipo de archivo, asi que unicamente se requiere del nombre y ubicacion del mismo para permitir que otras clases trabajen con archivos de manera genérica y flexible.Esto facilita la extensión y el mantenimiento, ya que el resto del sistema no depende de detalles concretos, cumpliendo así con el Principio de Inversión de Dependencias (DIP).

