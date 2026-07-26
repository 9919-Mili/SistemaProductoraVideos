# Encapsulamiento

El encapsulamiento consiste en proteger el estado interno de los objetos y controlar cómo se accede o modifica su información. En lugar de permitir el acceso directo a los atributos, cada clase expone únicamente los métodos necesarios para interactuar con ellos. De esta manera, los detalles internos permanecen ocultos y cada objeto es responsable de mantener la consistencia de su propio estado.

En el diagrama UML este principio se identifica mediante atributos privados (−) y operaciones públicas (+), lo que indica que la interacción con los datos se realiza a través de los métodos definidos por cada clase.

Desde el punto de vista de los principios **SOLID**, el encapsulamiento se relaciona principalmente con:

- **Single Responsibility Principle (SRP):** cada clase administra y protege únicamente su propio estado y comportamiento.
- **Open/Closed Principle (OCP):** la implementación interna puede modificarse sin afectar a las clases que utilizan sus métodos públicos.
- **Dependency Inversion Principle (DIP):** al ocultar los detalles internos de implementación, las demás clases interactúan únicamente mediante la interfaz pública de cada objeto, reduciendo el acoplamiento entre componentes.

---

## Ejemplo en el proyecto

En el sistema de gestión de la productora de videos, el encapsulamiento se observa principalmente en las clases **Proyecto**, **Etapa** y **Usuario**.

La clase **Proyecto** protege atributos como el responsable general, las fechas del proyecto, las etapas y los clientes asociados. Estos datos únicamente pueden modificarse mediante operaciones específicas como `registrarFechas()`, `asignarResponsable()` o `gestionarEtapas()`, evitando modificaciones directas desde otras clases.

La clase **Etapa** encapsula su estado interno, el responsable asignado, las observaciones y los archivos adjuntos. Cualquier cambio se realiza mediante métodos como `actualizarEstado()`, `agregarObservacion()` y `agregarAdjunto()`, permitiendo validar la información antes de modificar el objeto.

Por su parte, la clase **Usuario** mantiene protegida información sensible como las credenciales y administra internamente las notificaciones y los proyectos asignados mediante métodos públicos como `autenticar()`, `consultarProyectosAsignados()` y `recibirNotificacion()`.

### Fragmento del diagrama UML

![Diagrama Encapsulamiento](/diagramas/01-diagrama-clases/diagrama-doo-encapsulamiento-156880.png)

[➡ Ver diagrama completo en detalle](/diagramas/01-diagrama-clases/01-diagrama-clases-final.png)

### Justificación técnica

El fragmento del diagrama muestra que las clases Proyecto, Etapa y Usuario mantienen sus atributos privados y exponen únicamente los métodos necesarios para interactuar con ellos. Este diseño favorece el encapsulamiento, ya que protege la información interna de los objetos y permite controlar cómo se modifica su estado.

Además, facilita el mantenimiento del sistema y reduce el acoplamiento entre sus componentes.

---

## Ejemplo de Código

```
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
```

### Justificación técnica

Este fragmento aplica el principio de encapsulamiento porque los atributos permanecen privados y solo pueden modificarse mediante métodos públicos definidos por la propia clase. De esta manera, Proyecto controla su estado interno y evita modificaciones directas desde otras clases, favoreciendo la consistencia de la información y el mantenimiento del sistema.

```
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
```

### Justificación técnica

La clase Usuario mantiene protegida su información interna y permite interactuar con ella únicamente mediante métodos públicos. Esto evita modificaciones directas sobre sus datos, mejora la organización del código y facilita la evolución del sistema sin afectar al resto de las clases.