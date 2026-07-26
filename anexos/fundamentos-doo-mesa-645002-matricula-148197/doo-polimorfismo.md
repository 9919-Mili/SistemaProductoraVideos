## Polimorfismo

Permite que distintos objetos que comparten la misma interfaz respondan de manera diferente al mismo mensaje.

Su importancia en diseño orientado a objetos es que favorece la extension del sistema y permite construir modulos genericos que trabajan contra contratos estables.

Se relaciona con SOLID de la siguiente manera:

- **OCP (Open/Closed Principle):** Se agregan nuevos comportamientos incorporando nuevas implementaciones, sin cambiar codigo cliente.
- **LSP (Liskov Substitution Principle):** Cualquier subtipo debe poder sustituir al tipo base manteniendo comportamiento valido.
- **DIP (Dependency Inversion Principle):** Los modulos de alto nivel dependen de abstracciones, no de clases concretas.

En patrones de diseño, el polimorfismo es base de **Observer** (multiples observadores reaccionan al mismo evento mediante una interfaz comun) y **Strategy** (distintas estrategias comparten una operacion comun con implementaciones diferentes).


## Ejemplo en el proyecto

Para evidenciar polimorfismo en el proyecto, se toma el diagrama del patron Observer aplicado al sistema:

- El contrato `Observer` define `actualizar(subject)`.
- `ServicioNotificaciones`, `ResponsableDelProyecto`, `Coordinador` y `DashboardAdministrador` implementan ese contrato con respuestas distintas.

![Diagrama UML de polimorfismo (Observer)](/diagramas/01-diagrama-clases/01-patron-comportamiento-observer.png)

[Ver diagrama en detalle (PlantUML)](/diagramas/01-diagrama-clases/01-patron-comportamiento-observer.puml)

Este diagrama refleja polimorfismo porque un mismo mensaje (`actualizar`) se despacha a multiples implementaciones concretas. Tecnica y funcionalmente, cumple el fundamento porque:

- El sujeto maneja colecciones de `Observer`, no tipos concretos.
- Cada observador redefine su reaccion sin afectar el contrato.
- Se pueden sumar observadores nuevos sin modificar el flujo de notificacion.
- El sistema delega comportamiento segun tipo real en tiempo de ejecucion.

## Ejemplo de codigo

```java
import java.util.ArrayList;
import java.util.List;

interface Observer {
	void actualizar(String evento, Etapa etapa);
}

class ServicioNotificaciones implements Observer {
	@Override
	public void actualizar(String evento, Etapa etapa) {
		System.out.println("[Email/WhatsApp] " + evento + " en etapa: " + etapa.getNombre());
	}
}

class DashboardAdministrador implements Observer {
	@Override
	public void actualizar(String evento, Etapa etapa) {
		System.out.println("[Dashboard] Refrescar metricas por: " + evento);
	}
}

class ResponsableDelProyecto implements Observer {
	@Override
	public void actualizar(String evento, Etapa etapa) {
		System.out.println("[Responsable] Revisar cambios en: " + etapa.getNombre());
	}
}

class Etapa {
	private String nombre;
	private String estado;
	private List<Observer> observers = new ArrayList<>();

	public Etapa(String nombre) {
		this.nombre = nombre;
		this.estado = "Pendiente";
	}

	public String getNombre() {
		return nombre;
	}

	public void agregarObserver(Observer observer) {
		observers.add(observer);
	}

	public void actualizarEstado(String nuevoEstado) {
		this.estado = nuevoEstado;
		notificar("Estado actualizado a " + nuevoEstado);
	}

	private void notificar(String evento) {
		for (Observer observer : observers) {
			observer.actualizar(evento, this);
		}
	}
}
```

Justificacion tecnica:

- El cliente (`Etapa`) opera con la abstraccion `Observer`, no con implementaciones concretas.
- La llamada uniforme `actualizar(...)` produce comportamientos diferentes segun el objeto real.
- Agregar una nueva reaccion (por ejemplo, `Coordinador`) no requiere cambiar la logica de notificacion.
- Se cumple sustitucion y extension segura del sistema bajo un contrato comun.

Por lo tanto, el fragmento cumple polimorfismo porque aplica despacho dinamico sobre una interfaz compartida y permite variacion de comportamiento sin modificar el modulo emisor.
