## Encapsulamiento

El encapsulamiento es el principio de la programacion orientada a objetos que protege el estado interno de una clase y expone solo lo necesario. 

Su importancia en el diseno orientado a objetos es que evita modificaciones invalidas, reduce acoplamiento y mejora la mantenibilidad. En vez de permitir acceso directo a los datos, la clase define reglas claras para leer o actualizar su informacion.

Se relaciona con los principios SOLID de la siguiente manera:

- **SRP (Single Responsibility Principle):** cada clase concentra la responsabilidad de proteger su propio estado y reglas.
- **OCP (Open/Closed Principle):** Al ocultar detalles internos, se pueden extender comportamientos sin exponer ni romper el nucleo de datos.
- **ISP (Interface Segregation Principle):** Se publican interfaces pequeñas con solo las operaciones necesarias, sin obligar a depender de metodos innecesarios.


## Ejemplo en el proyecto

Para evidenciar encapsulamiento en el proyecto, se toma el diagrama final de clases, donde los atributos estan marcados como privados (`-`) y los metodos publicos (`+`) controlan la interaccion:

- `Proyecto`, `Etapa`, `Observacion` y `Adjunto` conservan sus datos internos no expuestos directamente.
- La modificacion de estado se realiza por operaciones del dominio como `actualizarEstado`, `asignarResponsable` o `agregarObservacion`.

![Diagrama UML de encapsulamiento (version final)](/diagramas/01-diagrama-clases/01-diagrama-clases-final.png)

[Ver diagrama en detalle (PlantUML)](/diagramas/01-diagrama-clases/01-diagrama-clases-final.puml)

El diagrama refleja encapsulamiento porque separa claramente datos internos de la interfaz publica de uso. Tecnica y funcionalmente, esto cumple el fundamento porque:

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
