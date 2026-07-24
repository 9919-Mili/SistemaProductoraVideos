# Encapsulamiento

El encapsulamiento en este proyecto se aplica como un mecanismo de control del estado interno de las entidades principales del sistema. No se trata únicamente de ocultar atributos, sino de garantizar que cualquier modificación del modelo pase por reglas definidas por la propia clase. De esta manera, los detalles internos de implementación permanecen ocultos y el resto del sistema interactúa únicamente a través de una interfaz pública controlada.

Este principio no solo protege los atributos de una clase, sino que también permite que cada objeto sea responsable de mantener la consistencia de su propio estado. Gracias al encapsulamiento, las reglas de negocio permanecen centralizadas dentro de la clase correspondiente, evitando modificaciones externas que puedan producir inconsistencias o comportamientos inesperados.

El diseño implementado evita estos problemas restringiendo el acceso directo a los atributos y obligando a interactuar mediante métodos públicos que contienen lógica interna y validaciones.
Desde el punto de vista de los principios **SOLID**, el encapsulamiento se relaciona principalmente con:

- **Single Responsibility Principle (SRP):** cada clase administra y protege únicamente su propio estado y comportamiento.
- **Open/Closed Principle (OCP):** la implementación interna puede modificarse sin afectar a las clases que utilizan sus métodos públicos.
- **Dependency Inversion Principle (DIP):** al ocultar los detalles internos de implementación, las demás clases interactúan únicamente mediante la interfaz pública de cada objeto, reduciendo el acoplamiento entre componentes.

Asimismo, el encapsulamiento constituye un elemento fundamental de los patrones de diseño implementados en el proyecto. En el patrón **Observer**, cada objeto observable administra internamente la colección de observadores y controla cuándo notificar a sus observadores. En **Factory Method**, la creación de objetos queda encapsulada dentro de las clases creadoras, evitando que el resto del sistema conozca los detalles del proceso de instanciación. En **Composite**, cada componente administra su propia estructura interna sin exponer cómo se organizan sus elementos.

---

## Ejemplo en el proyecto

En el sistema de gestión de la productora de videos, el encapsulamiento se observa principalmente en las clases **Proyecto**, **Etapa** y **Usuario**.

La clase **Proyecto** protege atributos como el responsable general, las fechas del proyecto, las etapas y los clientes asociados. Estos datos únicamente pueden modificarse mediante operaciones específicas como `registrarFechas()`, `asignarResponsable()` o `gestionarEtapas()`, evitando modificaciones directas desde otras clases.

La clase **Etapa** encapsula su estado interno, el responsable asignado, las observaciones y los archivos adjuntos. Cualquier cambio se realiza mediante métodos como `actualizarEstado()`, `agregarObservacion()` y `agregarAdjunto()`, permitiendo validar la información antes de modificar el objeto.

Por su parte, la clase **Usuario** mantiene protegida información sensible como las credenciales y administra internamente las notificaciones y los proyectos asignados mediante métodos públicos como `autenticar()`, `consultarProyectosAsignados()` y `recibirNotificacion()`.

### Fragmento del diagrama UML

![Diagrama Encapsulamiento](/diagramas/01-diagrama-clases/01-doo-encapsulamiento.png)

[Ver diagrama en detalle](/diagramas/01-diagrama-clases/01-doo-encapsulamiento.puml)

### Justificación técnica

El fragmento seleccionado muestra cómo las clases **Proyecto**, **Etapa** y **Usuario** mantienen sus atributos protegidos y exponen únicamente los métodos necesarios para interactuar con ellos. Ninguna clase externa modifica directamente los datos internos; todas las operaciones pasan por métodos públicos que permiten aplicar validaciones y reglas de negocio antes de actualizar el estado de los objetos.

Este diseño reduce el acoplamiento entre componentes, facilita el mantenimiento del sistema y permite modificar la implementación interna sin afectar a las demás clases que utilizan estas entidades.

---

## Ejemplo de Código

public class Proyecto {

    private String nombre;
    private String tipo;
    private Date fechaInicio;
    private Date fechaFin;
    private Usuario responsableGeneral;
    private List<Etapa> etapas;
    private List<Cliente> clientes;

    public void registrarFechas(Date inicio, Date fin) {
        // Validación de fechas
    }

    public void asignarResponsable(Usuario responsable) {
        this.responsableGeneral = responsable;
    }

    public void gestionarEtapas() {
        // Administración de etapas
    }
}

### Justificación técnica

Este fragmento aplica el principio de encapsulamiento porque todos los atributos permanecen privados y únicamente pueden modificarse mediante métodos públicos definidos por la propia clase. De esta forma, `Proyecto` controla sus reglas de negocio antes de actualizar su estado interno, evitando modificaciones arbitrarias y garantizando la consistencia de la información. Además, futuras modificaciones en la implementación podrán realizarse sin afectar a las clases que utilizan esta entidad.

public class Usuario {

    private String nombre;
    private String rol;
    private String credenciales;
    private List<Proyecto> proyectos;
    private List<Notificacion> notificaciones;

    public boolean autenticar(String email, String password) {
        // Validación de credenciales
        return true;
    }

    public List<Proyecto> consultarProyectosAsignados() {
        return proyectos;
    }

    public void recibirNotificacion(Notificacion notificacion) {
        notificaciones.add(notificacion);
    }
}

### Justificación técnica

La clase `Usuario` encapsula la información personal, las credenciales y las relaciones con otros elementos del sistema. Los atributos permanecen protegidos y solo pueden ser utilizados mediante métodos públicos que controlan su acceso. Esto evita modificaciones indebidas sobre información sensible, reduce el acoplamiento entre clases y permite que la implementación interna evolucione sin afectar al resto del sistema, favoreciendo el mantenimiento, la reutilización y la escalabilidad del software.