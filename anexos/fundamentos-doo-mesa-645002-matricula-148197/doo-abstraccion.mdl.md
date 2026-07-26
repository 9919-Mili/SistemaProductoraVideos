## Abstracción

La abstracción es el principio que permite modelar solo las características esenciales de un objeto y ocultar los detalles internos que no son necesarios para su uso. En diseño orientado a objetos, esto ayuda a construir clases más simples, legibles y reutilizables.

Su importancia está en que reduce la complejidad del sistema y facilita el mantenimiento. Cuando un componente depende de abstracciones en lugar de depender de clases concretas, el código se vuelve más flexible y más fácil de extender sin romper lo que ya se encuentra registrado. 

Se relaciona directamente con SOLID sobre todo con el principio de inversión de dependencias, porque promueve que los módulos de alto nivel trabajen con interfaces o clases bases. También apoya el principio de responsabilidad única, ya que cada clase o interfaz representa una sola idea del dominio.

En los patrones de diseño, la abstracción aparece cuando se quieren ocultar detalles que son complejos, para exponer solo lo esencial. 


## Ejemplo en el proyecto
El diagrama que mejor refleja la abstracción en este proyecto es el de DIP, porque separa a la clase `Etapa` de los detalles concretos de implementación y la hace depender de interfaces.

![Diagrama DIP - Abstracciones para clase Etapa](/diagramas/01-diagrama-clases/01-solid-05-dip.png)

[Ver diagrama en detalle](/diagramas/01-diagrama-clases/01-solid-05-dip.puml)

En este diagrama, `Etapa` trabaja con `IExtractorNombre` e `IAgregarObjeto` en lugar de acoplarse directamente a `Usuario`, `Observacion` o `Adjunto`. Eso refleja abstracción porque la clase usa contratos estables y oculta la implementación concreta detrás de esas interfaces.

Técnicamente, esto cumple el fundamento porque `Etapa` puede coordinar observaciones, adjuntos y responsables sin conocer cómo se resuelve cada operación por dentro. De esa forma, el diseño reduce dependencias rígidas, mejora la reutilización y facilita cambios futuros sin modificar la clase principal.

## Ejemplo de Código
```java
interface IExtractorNombre {
	String obtenerNombre();
}

interface IAgregarObjeto {
	void agregarObjeto();
}

class Usuario implements IExtractorNombre {
	private String nombre;

	public Usuario(String nombre) {
		this.nombre = nombre;
	}

	@Override
	public String obtenerNombre() {
		return nombre;
	}
}

class Observacion implements IAgregarObjeto {
	private String texto;
	private IExtractorNombre autor;

	public Observacion(String texto, IExtractorNombre autor) {
		this.texto = texto;
		this.autor = autor;
	}

	@Override
	public void agregarObjeto() {
		System.out.println("Observacion registrada por: " + autor.obtenerNombre());
	}
}

class Adjunto implements IAgregarObjeto {
	private String url;

	public Adjunto(String url) {
		this.url = url;
	}

	@Override
	public void agregarObjeto() {
		System.out.println("Adjunto agregado: " + url);
	}
}

class Etapa {
	private IExtractorNombre responsableEtapa;
	private List<IAgregarObjeto> elementos;

	public Etapa(IExtractorNombre responsableEtapa, List<IAgregarObjeto> elementos) {
		this.responsableEtapa = responsableEtapa;
		this.elementos = elementos;
	}

	public void agregarObservacionYAdjunto() {
		for (IAgregarObjeto elemento : elementos) {
			elemento.agregarObjeto();
		}
	}
}
```

Este fragmento cumple con la abstracción porque `Etapa` no depende de clases concretas, sino de contratos (`IExtractorNombre` e `IAgregarObjeto`). Por eso puede trabajar con distintos tipos de objetos (por ejemplo `Observacion` y `Adjunto`) sin cambiar su lógica interna.

Justificación técnica: 

- Se desacopla el módulo de alto nivel (`Etapa`) de los módulos de detalle. Esto reduce el impacto de cambios, facilita pruebas y mantiene el diseño extensible, en línea con el fundamento de abstracción y el principio DIP de SOLID.