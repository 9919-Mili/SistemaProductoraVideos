## Herencia

La herencia permite crear una clase nueva a partir de otra ya existente, reutilizando su estructura y comportamiento común.

Su importancia en diseño orientado a objetos está en que evita duplicación, mejora la consistencia de reglas de negocio y facilita la extensibilidad del sistema. En lugar de repetir lógica en varias clases, se centraliza en una superclase y las subclases representan variantes concretas del mismo concepto del dominio.

La herencia se relaciona con la abstracción porque normalmente parte de clases base abstractas que definen contratos y comportamiento común. También se conecta con SOLID:

- **OCP (Open/Closed Principle):** Se agregan nuevas subclases sin modificar la clase base.

- **LSP (Liskov Substitution Principle):** Cualquier subclase debe poder reemplazar a la superclase sin romper el sistema.

- **DIP (Dependency Inversion Principle):** Los módulos de alto nivel pueden depender de la superclase abstracta en lugar de implementaciones concretas.

En patrones de diseño, esta combinación de abstracción + herencia aparece con frecuencia en **Template Method** (flujo común en la superclase y pasos variables en subclases) y puede complementarse con **Factory Method** para instanciar subclases según contexto.

## Ejemplo en el proyecto

Para evidenciar herencia en el proyecto se toma la jerarquía de notificaciones modelada en el diagrama de LSP:

- `Notificacion` (abstracta) define comportamiento común.
- `NotificacionEmail`, `NotificacionWhatsApp` y `NotificacionSMS` extienden esa base y especializan el envío por canal.

![Diagrama UML de herencia (LSP)](/diagramas/01-diagrama-clases/01-solid-03-lsp.png)

[Ver diagrama en detalle (PlantUML)](/diagramas/01-diagrama-clases/01-solid-03-lsp.puml)

Este diagrama refleja herencia porque muestra una superclase abstracta con atributos y operaciones comunes, y múltiples subclases que mantienen el contrato pero redefinen comportamiento específico. Desde el punto de vista técnico, cumple el fundamento porque:

- Existe una relación **es-un**: `NotificacionEmail` es una `Notificacion`, etc.
- Las subclases heredan estado y operaciones base, evitando duplicación.
- Las variaciones de comportamiento se implementan por sobrescritura, sin alterar el cliente.
- El sistema puede operar contra la abstracción (`Notificacion`) y no contra tipos concretos.

## Ejemplo de código

```java
import java.util.List;

abstract class Notificacion {
	protected String mensaje;
	protected Usuario destinatario;

	public Notificacion(String mensaje, Usuario destinatario) {
		this.mensaje = mensaje;
		this.destinatario = destinatario;
	}

	// Template Method: flujo comun para cualquier canal de notificacion.
	public final void enviar() {
		if (!validarDisponibilidad()) {
			throw new IllegalStateException("Canal no disponible");
		}
		realizarEnvio();
		registrarEnvio();
	}

	protected abstract boolean validarDisponibilidad();
	protected abstract void realizarEnvio();

	protected void registrarEnvio() {
		System.out.println("Notificacion enviada a " + destinatario.getNombre());
	}
}

class NotificacionEmail extends Notificacion {
	public NotificacionEmail(String mensaje, Usuario destinatario) {
		super(mensaje, destinatario);
	}

	@Override
	protected boolean validarDisponibilidad() { return true; }

	@Override
	protected void realizarEnvio() {
		System.out.println("Enviando EMAIL: " + mensaje);
	}
}

class NotificacionWhatsApp extends Notificacion {
	public NotificacionWhatsApp(String mensaje, Usuario destinatario) {
		super(mensaje, destinatario);
	}

	@Override
	protected boolean validarDisponibilidad() { return true; }

	@Override
	protected void realizarEnvio() {
		System.out.println("Enviando WHATSAPP: " + mensaje);
	}
}

class Usuario {
	private String nombre;

	public Usuario(String nombre) {
		this.nombre = nombre;
	}

	public String getNombre() {
		return nombre;
	}
}

class Sistema {
	public void notificarUsuarios(List<Notificacion> notificaciones) {
		for (Notificacion notificacion : notificaciones) {
			notificacion.enviar();
		}
	}
}
```

Justificacion tecnica:

- El modulo de alto nivel (`Sistema`) depende de la abstraccion (`Notificacion`) y no de clases concretas.
- Cada subclase extiende comportamiento heredado sin romper el contrato base (LSP).
- Para agregar un nuevo canal (por ejemplo `NotificacionPush`), basta con crear otra subclase (OCP).
- La reutilizacion del flujo comun (`enviar`) reduce duplicacion y mantiene consistencia en reglas de envio.

Por lo tanto, el fragmento cumple herencia como fundamento DOO porque utiliza una jerarquia real de clases con especializacion de comportamiento, sustitucion polimorfica y extension segura del modelo.
