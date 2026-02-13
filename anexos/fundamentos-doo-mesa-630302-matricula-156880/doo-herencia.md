# Herencia

La herencia permite modelar relaciones de generalización y especialización dentro de un sistema orientado a objetos. A través de ella, una clase base define características comunes que luego pueden ser reutilizadas y extendidas por clases más específicas.

En este proyecto, la herencia no se utiliza simplemente para reutilizar código, sino para representar correctamente una relación conceptual del dominio: un archivo genérico y su especialización como archivo adjunto dentro de una etapa del proyecto.

---

## Aplicación en el Modelo

Dentro del Sistema Productora de Videos se define una jerarquía compuesta por:

- `Archivo` (clase base abstracta)
- `Adjunto` (clase derivada)

La clase `Archivo` representa una abstracción general de cualquier recurso almacenado en el sistema. Contiene atributos comunes como:

- `nombreArchivo`
- `ubicacion`

Al declararse como clase abstracta, establece que no debe instanciarse directamente, sino que funciona como una base para tipos más específicos.

Por otro lado, `Adjunto` extiende a `Archivo`, incorporando comportamiento y atributos propios del contexto de una etapa de proyecto, como:

- `url`
- `descripcion`
- Método `vincularRecurso()`

Esto implica que todo `Adjunto` es un `Archivo`, pero no todo `Archivo` necesariamente es un `Adjunto`.

---

## Justificación de Diseño

La utilización de herencia en este caso responde a varias decisiones de diseño:

1. **Representación correcta del dominio:**  
   Conceptualmente, un adjunto es un tipo particular de archivo. Modelarlo mediante herencia refleja esta relación "es-un".

2. **Reutilización estructural:**  
   Los atributos comunes no se duplican en cada clase concreta, sino que se definen una sola vez en `Archivo`.

3. **Extensibilidad futura:**  
   Si en el futuro se necesitara incorporar nuevos tipos como `ArchivoTemporal` o `ArchivoExterno`, podrían agregarse como nuevas subclases sin modificar la clase base.

4. **Polimorfismo:**  
   Permite tratar instancias de `Adjunto` como instancias de `Archivo`, facilitando el manejo genérico de archivos en el sistema.

---

## Relación con Principios de Diseño

La jerarquía respeta principalmente:

- **OCP (Open/Closed Principle):**  
  Se pueden agregar nuevas especializaciones sin alterar la clase base.

- **LSP (Liskov Substitution Principle):**  
  Un objeto `Adjunto` puede utilizarse donde se espere un `Archivo`, sin romper el comportamiento del sistema.

Además, al trabajar sobre la abstracción `Archivo`, se favorece un menor acoplamiento entre componentes.

---

## Ejemplo de Código Representativo

```java
public abstract class Archivo {

    protected String nombreArchivo;
    protected String ubicacion;

    public String obtenerNombre() {
        return nombreArchivo;
    }

    public String obtenerUbicacion() {
        return ubicacion;
    }
}
