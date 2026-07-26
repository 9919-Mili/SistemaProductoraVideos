# Polimorfismo

El polimorfismo permite que distintos objetos puedan responder de manera diferente a una misma operación utilizando una referencia común. De esta forma, las clases trabajan sobre abstracciones en lugar de depender de implementaciones concretas, favoreciendo un diseño más flexible y fácil de extender.

En el sistema de gestión de la productora de videos, este principio se aplica mediante el patrón Observer, donde distintos observadores implementan un mismo contrato y responden de forma diferente cuando se produce un evento dentro del sistema.

Desde el punto de vista de los principios SOLID, el polimorfismo se relaciona principalmente con:

- **Open/Closed Principle (OCP):** permite incorporar nuevas implementaciones sin modificar las clases que trabajan con la abstracción.
- **Liskov Substitution Principle (LSP):** cualquier implementación de Observer puede sustituir a otra sin afectar el funcionamiento esperado.
- **Dependency Inversion Principle (DIP):** las clases dependen de la abstracción Observer y no de implementaciones concretas.

---

## Ejemplo en el proyecto

En el proyecto, el polimorfismo se observa en la implementación del patrón Observer.

La interfaz Observer define la operación actualizar(), mientras que las clases ServicioNotificaciones, ResponsableDelProyecto, Coordinador y DashboardAdministrador implementan ese mismo método con comportamientos diferentes.

De esta manera, la clase que genera las notificaciones trabaja con la abstracción Observer, sin depender de una implementación concreta, permitiendo incorporar nuevos observadores sin modificar el funcionamiento del sistema.

### Fragmento del diagrama UML
```
@startuml

interface Subject {
    +agregarObserver(o : Observer)
    +quitarObserver(o : Observer)
    +notificar()
}

interface Observer {
    +actualizar(subject : Subject)
}

abstract class ElementoObservable {
    -observadores : List<Observer>
    +agregarObserver(o : Observer)
    +quitarObserver(o : Observer)
    +notificar()
}

class Proyecto
class Etapa
class Tarea

class ServicioNotificaciones {
    +actualizar(subject : Subject)
}

class ResponsableDelProyecto {
    +actualizar(subject : Subject)
}

class Coordinador {
    +actualizar(subject : Subject)
}

class DashboardAdministrador {
    +actualizar(subject : Subject)
}

ElementoObservable ..|> Subject
Proyecto ..|> ElementoObservable
Etapa ..|> ElementoObservable
Tarea ..|> ElementoObservable

ServicioNotificaciones ..|> Observer
ResponsableDelProyecto ..|> Observer
Coordinador ..|> Observer
DashboardAdministrador ..|> Observer

Subject "1" o-- "*" Observer

@enduml
```

![Diagrama Polimorfismo](/diagramas/01-diagrama-clases/01-patron-comportamiento-observer.png)

[➡ Ver diagrama completo en detalle](/diagramas/01-diagrama-clases/01-patron-comportamiento-observer.puml)

### Justificación técnica

El diagrama muestra que varias clases implementan la interfaz Observer y comparten la operación actualizar(). Aunque todas responden al mismo mensaje, cada una puede ejecutar un comportamiento diferente según su implementación. Esto permite que el sistema trabaje con la abstracción Observer sin depender de clases concretas, facilitando la incorporación de nuevos observadores sin modificar la lógica de notificación.

---

## Ejemplo de Código
```
interface Observer {
    void actualizar(String evento);
}

class ServicioNotificaciones implements Observer {

    @Override
    public void actualizar(String evento) {
        System.out.println("Enviando notificación: " + evento);
    }
}

class DashboardAdministrador implements Observer {

    @Override
    public void actualizar(String evento) {
        System.out.println("Actualizando dashboard: " + evento);
    }
}

class ResponsableDelProyecto implements Observer {

    @Override
    public void actualizar(String evento) {
        System.out.println("Revisando evento: " + evento);
    }
}

Observer observer = new ServicioNotificaciones();
observer.actualizar("Etapa finalizada");
```

### Justificación técnica

Este fragmento demuestra el principio de polimorfismo porque la variable observer está declarada como tipo Observer, mientras que el objeto utilizado corresponde a una implementación concreta. Al invocar el método actualizar(), cada implementación ejecuta un comportamiento diferente según el tipo de objeto que la recibe. De esta manera, el sistema puede trabajar con distintos observadores mediante una misma referencia, facilitando la incorporación de nuevas implementaciones sin modificar la lógica de notificación.