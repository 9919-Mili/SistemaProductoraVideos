# Anexo – Aplicación de Patrón de Diseño de Estructural – Composite

## Patrones  de  Diseño  Estructurales  y  su  relación con SOLID 

Los patrones de diseño estructurales organizan cómo se conectan y componen clases y objetos para construir sistemas más modulares y manejables: definen responsabilidades claras entre elementos, introducen niveles de indirection y permiten combinar componentes sin acoplarlos fuertemente.  
La estructura técnica que se aplica siguiendo estos modelos facilita cumplir las metas de SOLID porque actúa sobre las mismas propiedades que esos principios promueven —acoplamiento, cohesión, extensibilidad y claridad de contratos— pero desde una perspectiva orientada al sistema en lugar de cambios puntuales en una clase.

---

## Propósito y Tipo del Patrón


**Propósito:** La clase `Etapa`posee diferentes listas de objetos que se manejan de manera separada, lo que genera que duplicación de código y dificulta implementar nuevas extensiones que puedan añadirse a la clase `Etapa`, el patron de diseño a implementar pemite que objetos individuales (hojas) y composiciones de objetos (compuestos) sean tratados de manera uniforme mediante una interfaz común.

**Tipo:** Composite, permite tratar objetos individuales y colecciones de objetos de la misma manera mediante una interfaz común: las hojas (elementos atómicos) y los compuestos (contenedores de elementos) implementan el mismo contrato, de modo que el cliente no necesita distinguir entre un objeto simple y una composición de objetos para realizar operaciones (agregar, eliminar, operar).

---

## Motivación

- La clase `Etapa` contenía colecciones de objetos separadas: `observaciones: List<Observacion>` y `adjuntos: List<Adjunto>`. Para cada tipo existían métodos concretos (`agregarObservacion`, `modificarObservacion`, `agregarAdjunto`,).
- Se daban problemas los siguientes problemas de rigidez en las relaciones entre clases:
  - **Duplicación de código:** operaciones comunes (agregar, eliminar, modificar/actualizar) estaban replicadas por tipo, lo que incrementaba el esfuerzo al corregir o extender comportamiento.
  - **Acoplamiento fuerte:** `Etapa` y capas superiores debían conocer detalles de implementación de cada tipo de elemento; cambiar la estructura interna implicaba tocar múltiples clases.
  - **Falta de extensibilidad:** introducir un nuevo tipo de elemento (p. ej. `DescargaDeArchivo`) requería editar `Etapa`.
- Clases que participaban en el problema original:
  - `Etapa`: clase principal con listas de elementos separadas.
  - `Observacion`: clase de instancias con metodos exclusivos.
  - `Adjunto`: clase de instancias con metodos exclusivos.
- Nuevas clases introducidas por el patrón y el rol de cada una
  - `IAgregarObjeto`: define un contrato común para las clases usadas en la lista de Etpa permitiendo uniformidad y sustitución.
  - `ColeccionObjetos`: implementa `IAgregarObjeto`, sirve como una clase gestionadora de operaciones qur permite anidamiento.
  - `PlataformaEnLinea`: clase extendida de un compuesto elementos de lista para ejemplificar la implementacion de nuevos elementos.
  - `ArchivoVisibleEnLinea`: clase extendida de un compuesto elementos de lista para ejemplificar la implementacion de nuevos elementos.
  - `DescargaDeArchivo`: clase extendida de un compuesto elementos de lista para ejemplificar la implementacion de nuevos elementos.
- El patrón organiza la arquitectura al permitir que la clase `Etapa` deje de conocer tipos concretos y depende de la abstracción `IAgregarObjeto` (DIP), reduciendo acoplamiento, tambien reduce su superficie a pocos métodos (`agregarComponente`, `quitarComponente`, `modificarComponente`), evitando la duplicación de código. La clases que implementan `IAgregarObjeto` y se integran sin modificar `Etapa` para permitir un mayot nivel de extensibilidad. 

En el sistema de la Productora de Videos, la clase `Etapa` debe manejar diferentes elementos asociados: observaciones y adjuntos (links, archivos). Actualmente la arquitectura tiende a tratar observaciones y adjuntos con código y métodos distintos. Esto genera duplicación de lógica cuando se agregan, eliminan o listan estos elementos, y aumenta la complejidad en caso de añadir nuevos tipos de objetos que deberían ser gestionados por una etapa (por ejemplo: links de descarga, archivos almacenados).

Problema concreto: la clase `Etapa` necesita una forma uniforme de agregar/quitar/mostrar elementos asociados (observaciones, adjuntos, colecciones de ambos), sin proliferar métodos especializados y con bajo acoplamiento.

Se propone aplicar el patrón estructural **Composite**. Con él, `Observacion` y `Adjunto` implementan la misma interfaz `IAgregarObjeto` y pueden ser tratados indistintamente. Además se introduce una clase compuesta (`ColeccionObjetos`) que agrupa varios `IAgregarObjeto` y delega operaciones a sus "hijos".

---


## Estructura de Clases (UML)

La siguiente imagen muestra la estructura propuesta aplicando **Composite**.

![Diagrama Composite](/diagramas/01-diagrama-clases/01-patron-estructural-composite.png)

[Ver Diagrama en Tamaño Completo](/diagramas/01-diagrama-clases/01-patron-estructural-composite.png)

---

## Justificación Técnica de la Estructura de Clases 

La clase `Etapa` necesita una forma uniforme de agregar/quitar/modifiar elementos asociados (observaciones, adjuntos, colecciones de ambos), sin proliferar métodos especializados y con bajo acoplamiento.

- **Clases incluidas en el diagrama:**
  - `Etapa` (Clase/Contenedor):   
   Contiene referencia a `IAgregarObjeto` (por ejemplo una `ColeccionObjetos`) y expone métodos para agregar/quitar/modificar componentes. Clase principal para la que se aplica el Patron de Diseño.
  - `IAgregarObjeto` (Interfaz - componente):  
  Define `agregar()`, `eliminar()`, `modificar()`. Interfaz necesaria para establecer un contrato sobre las clases.
  - `ColeccionObjetos` (Composite):  
  Mantiene una lista de `IAgregarObjeto`; implementa las operaciones delegando a sus hijos. Permite la extracción/busqueda de cualquier elemento extendido por la interfaz.
  - `Observacion` (Hoja):  
  Implementa `IAgregarObjeto`, encapsula `texto`, `autor`, etc. Clase de elementos de lista.
  - `Adjunto` (Rama/Compuesto):  
  Implementa `IAgregarObjeto`, define los atributos `url`, `tipo`, metadatos. Superclase que hereda a algunas clases "hoja".
  - `PlataformaEnLinea` (Hoja):  
  Implementa `IAgregarObjeto`, encapsula `url`, `tipo`, etc. Clase de elementos de lista.
  - `ArchivoVisibleEnLinea` (Hoja):  
  Implementa `IAgregarObjeto`, encapsula `url`, `tipo`, etc. Clase de elementos de lista.
  - `DescargaDeArchivo` (Hoja):  
  Implementa `IAgregarObjeto`, encapsula `url`, `tipo`, etc. Clase de elementos de lista.

- **Explicación del flujo estructural:**

  La clase principal delega la gestión de los elementos asociados a una abstracción(Interfaz Componente) común en lugar de manejar tipos concretos; esa abstracción es la puerta de entrada para todas las operaciones de métodos sobre los elementos sin necesidad de conocer si el receptor es un elemento atómico(Hoja) o una colección de elementos(Compuesto).  

  Las implementaciones concretas que representan elementos individuales(Hoja) ejecutan la operación directamente, mientras que las implementaciones que representan colecciones(Compuesto) reparten la misma operación entre sus elementos contenidos(Hojas), reenviando o combinando resultados según sea necesario.   

  De este modo la operación queda distribuida: las hojas realizan el trabajo específico y los compuestos coordinan a sus hijos, lo que elimina duplicación, reduce el acoplamiento entre capas y permite agregar nuevos tipos de elementos sin cambiar la lógica de quien usa la abstracción.

- **Explicación técnica del caso y patron aplicado:**

  En la solución se aplicó el patrón Composite definiendo la interfaz `IAgregarObjeto` como el contrato común (que expone los métodos `agregar()`, `eliminar()` y `modificar()`). La clase `Etapa` interactúa únicamente con esa abstracción y delega la gestión de los elementos mediante operaciones de alto nivel como `agregarComponente`, `quitarComponente` y `modificarComponente`, sin conocer las implementaciones concretas.

  Las implementaciones que actúan como hojas —por ejemplo `Observacion`, que contiene atributos como `texto` y `autor`— realizan directamente las acciones requeridas;  
  Los elementos variantes de tipo adjunto (`Adjunto`) que son (`PlataformaEnLinea`, `ArchivoVisibleEnLinea`, `DescargaDeArchivo`) exponen atributos como `url`, `tipo` y `metadatos` y se integran implementando la misma interfaz, por lo que pueden ser tratados como "hojas" por la abstracción;   
  Las implementaciones que actúan como compuestos —representadas por `ColeccionObjetos`— mantienen internamente una colección de `IAgregarObjeto` y propagan las llamadas a cada hijo, combinando o reenviando resultados cuando procede.

  Con esta organización la responsabilidad de llevar a cabo operaciones compuestas queda localizada en `ColeccionObjetos`, mientras las hojas se ocupan de la lógica específica de su tipo. Así se elimina la duplicación de operaciones por tipo, se reduce el acoplamiento entre capas y se facilita añadir nuevos tipos de elementos (sólo deben implementar `IAgregarObjeto`) sin modificar la clase que coordina la colección.
