# Encapsulamiento


El encapsulamiento consiste en ocultar los detalles internos de una clase u objeto, exponiendo únicamente una interfaz pública que permite la interacción controlada con sus datos y comportamientos. De este modo, se protege la integridad de los atributos y se evita el acceso o modificación directa desde el exterior, permitiendo que los cambios internos no afecten a quienes utilizan la clase.

El encapsulamiento está estrechamente ligado a varios principios SOLID, ya que al restringir el acceso directo a los datos y obligar a interactuar mediante métodos específicos, se facilita la extensión sin modificar el código existente oculto **(OCP)**, y se promueve la segregación de interfaces **(ISP)** al exponer solo los métodos necesarios. Además, permite invertir dependencias **(DIP)** al delegar el interactuar a abstracciones en lugar de implementaciones concretas.

El encapsulamiento es fundamental en muchos patrones de diseño. Patrones creacionales como **Builder** y **Singleton** utilizan encapsulamiento para controlar la creación y el acceso a instancias. Patrones estructurales como **Facade** y **Decorator** aprovechan el encapsulamiento para simplificar o extender funcionalidades sin exponer detalles internos. Patrones de comportamiento como **Command** y **State** dependen del encapsulamiento para modificar el comportamiento de los objetos sin alterar su estructura interna.

## Ejemplo en el proyecto



**Clase `Proyecto`**

`Proyecto` encapsula los datos y operaciones relacionadas con la gestión de un proyecto audiovisual. Los atributos como su nombre y clientes están protegidos y solo pueden ser accedidos o modificados mediante métodos públicos.

**Métodos principales:** `crearProyecto()`, `consultarProyectosActivos()`, `asignarResponsable()`, `gestionarEtapas()`  
**Relaciones:** Gestiona instancias de `Etapa`, `Usuario` y `Cliente` internamente.

**Justificación técnica:** El encapsulamiento en `Proyecto` permite que la gestión de datos y operaciones se realice de forma controlada, evitando modificaciones directas y protegiendo la integridad del proyecto. Facilita la extensión y el mantenimiento, cumpliendo OCP.

---
**Clase `Etapa`**

`Etapa` encapsula el estado y los elementos asociados a una fase del proyecto, permitiendo el acceso y modificación solo a través de métodos públicos. Los atributos internos, como la lista de observaciones, adjuntos y el responsable, están protegidos y no pueden ser modificados directamente desde otras clases.

- **Métodos principales**: `actualizarEstado()`, `agregarObservaciones()`, `registrarAdjuntos()`
- **Relaciones**: Incluye instancias de `Observacion` `Adjunto` y un `Usuario` responsable, gestionados internamente.

**Justificación técnica:** El encapsulamiento en `Etapa` protege los datos internos y asegura que solo se acceda o modifique mediante métodos específicos, facilitando el mantenimiento y evitando errores por acceso indebido. Permite modificar la implementación interna sin afectar otras partes del sistema, cumpliendo con OCP.

---
**Clase `Usuario`**

`Usuario` encapsula la información personal y las credenciales de cada usuario, exponiendo solo métodos de acceso. Los atributos están protegidos y su acceso está restringido a través de la interfaz pública.

- **Atributos simples:** `nombre`, `rol`, `credenciales`, `proyectos`, `notificaciones`
- **Método esencial:** `autenticar()`, `consultarProyectosAsignados()`, `recibirNotificacion()`
- **Relación con otras clases:** Interactúa con `Proyecto`, `Etapa` y `Notificacion` mediante métodos definidos.

**Justificación técnica:** El encapsulamiento en Usuario protege la información sensible y asegura que solo se acceda mediante métodos específicos, evitando riesgos de seguridad y errores. Mientras que atributos como notificaciones y pryectos estan abiertos a modificacion mediante metodos externos, asi promueve bajo acoplamiento y facilita la extensión de funcionalidades (OCP).

## Ejemplo de Código

Esta parte del diagrama refleja la encapsulación de unas clases del Sistema Productora de Vídeos:

![Diagrama de Clases Final](/diagramas/01-diagrama-clases/diagrama-doo-encapsulacion.png)

[➡ Ver diagrama completo en detalle](/diagramas/01-diagrama-clases/01-diagrama-clases-final.puml)

```
class Proyecto {
    - nombre: string
    - tipo: string
    - fechaInicio: Date
    - fechaFin: Date
    - responsableGeneral: Usuario
    - etapas: List<Etapa>
    - clientes: List<Cliente>
    + crearProyecto(nombre: string, tipo: string, fechaInicio: Date, fechaFin: Date, responsable: Usuario): Proyecto
    + consultarProyectosActivos(): List<Proyecto>
    + asignarResponsable(responsable: Usuario): Usuario
    + gestionarEtapas(): void
    + consultarFechaInicio(): Date
    + consultarFechaEntrega(): Date
    + agregarObservaciones(nombre: string, descripcion: string): Observacion
    + registrarFechas(fechaInicio: Date, fechaFin: Date): bool
    + buscarCliente(nombre: string): string
}
```
Este fragmento de código cumple el fundamento de encapsulamiento al declarar los atributos de la clase Proyecto como su nombre y tipo privados, impidiendo el acceso directo desde otras clases. El acceso y modificación se realizan exclusivamente en determinados atributos como su responsable, etapas y clientes relacionados mediante métodos públicos como asignarResponsable y otros. Esto protege la integridad de la información, evita modificaciones no autorizadas y permite cambiar la implementación interna sin afectar a quienes utilizan la clase. Así, se promueve bajo acoplamiento, facilidad de mantenimiento y extensión, en línea con los principios SOLID (OCP, DIP).
```
class Usuario {
    - nombre: string
    - rol: string
    - credenciales: string
    - proyectos: List<Proyecto>
    - notificaciones: List<Notificacion>
    + autenticar(email: string, password: string): bool
    + consultarProyectosAsignados(): List<Proyecto>
    + recibirNotificacion(notificacion: Notificacion): void
}
```
Este fragmento de código cumple el fundamento de encapsulamiento al declarar algunos atributos de la clase Usuario como privados, impidiendo el acceso directo desde otras clases. El acceso de los datos se realiza exclusivamente mediante métodos públicos como autenticar() y consultarProyectosAsignados(). Esto protege la integridad de la información, evita modificaciones no autorizadas y permite el mantenimiento de otros atributos conforme a los principios SOLID (OCP, DIP).
