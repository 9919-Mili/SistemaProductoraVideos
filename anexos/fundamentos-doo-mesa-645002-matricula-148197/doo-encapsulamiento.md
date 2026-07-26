## Encapsulamiento

El encapsulamiento es el principio de la programacion orientada a objetos que protege el estado interno de una clase y expone solo lo necesario. 

Su importancia en el diseno orientado a objetos es que evita modificaciones invalidas, reduce acoplamiento y mejora la mantenibilidad. En vez de permitir acceso directo a los datos, la clase define reglas claras para leer o actualizar su informacion.

Se relaciona con los principios SOLID de la siguiente manera:

- **SRP (Single Responsibility Principle):** cada clase concentra la responsabilidad de proteger su propio estado y reglas.
- **OCP (Open/Closed Principle):** Al ocultar detalles internos, se pueden extender comportamientos sin exponer ni romper el nucleo de datos.
- **ISP (Interface Segregation Principle):** Se publican interfaces pequeñas con solo las operaciones necesarias, sin obligar a depender de metodos innecesarios.

En patrones de diseño, el encapsulamiento se aplica en **State** (cada estado encapsula reglas de transicion y comportamiento) y en **Facade** (una interfaz simple encapsula la complejidad de varios componentes internos).


## Ejemplo en el proyecto

Para evidenciar encapsulamiento en el proyecto, se toma una **seleccion de clases** del diagrama de SRP: `Etapa`, `GestorObservaciones`, `GestorAdjuntos`, `Observacion` y `Adjunto`. En este fragmento, la clase `Etapa` encapsula su estado principal y delega operaciones especificas en gestores cohesionados.

![Diagrama UML de encapsulamiento (clases seleccionadas)](/diagramas/01-diagrama-clases/01-solid-01-srp.png)

[Ver diagrama en detalle (PlantUML)](/diagramas/01-diagrama-clases/01-solid-01-srp.puml)

El diagrama refleja encapsulamiento porque separa claramente datos internos de la interfaz publica de uso y organiza responsabilidades para que cada clase controle su propia consistencia. Tecnica y funcionalmente, esto cumple el fundamento porque:

- Se protege la integridad del objeto al impedir acceso directo a atributos sensibles.
- La clase valida reglas antes de cambiar su estado interno.
- Las demas clases dependen de comportamiento publico, no de estructura interna.
- El impacto de cambios internos se mantiene local a cada clase.

## Ejemplo de codigo

```java
import java.util.Arrays;
import java.util.List;

class Etapa {
	private String nombre;
	private String estado;
	private Usuario responsable;

	private static final List<String> ESTADOS_VALIDOS =
		Arrays.asList("Pendiente", "En progreso", "Finalizada");

	public Etapa(String nombre, Usuario responsable) {
		this.nombre = nombre;
		this.estado = "Pendiente";
		this.responsable = responsable;
	}

	public String getNombre() {
		return nombre;
	}

	public String getEstado() {
		return estado;
	}

	public boolean actualizarEstado(String nuevoEstado, Usuario actor) {
		if (!actor.equals(responsable)) {
			return false;
		}
		if (!ESTADOS_VALIDOS.contains(nuevoEstado)) {
			return false;
		}
		if (estado.equals("Finalizada")) {
			return false;
		}
		estado = nuevoEstado;
		return true;
	}
}

class Usuario {
	private String nombre;

	public Usuario(String nombre) {
		this.nombre = nombre;
	}
}
```

Justificacion tecnica:

- El estado interno (`estado`, `responsable`) es privado y no puede mutarse desde fuera.
- Toda actualizacion pasa por `actualizarEstado`, que encapsula reglas de autorizacion y transicion.
- La clase preserva sus invariantes sin exponer logica interna al resto del sistema.
- Se reduce acoplamiento porque consumidores usan metodos publicos, no acceden a campos directos.

Por lo tanto, el fragmento cumple encapsulamiento porque combina ocultamiento de datos con control explicito de cambios de estado, alineado con el dominio del proyecto.
