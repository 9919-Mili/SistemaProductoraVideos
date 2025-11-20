# Principio de Sustitución de Liskov (LSP)

## Propósito y Tipo del Principio SOLID

El Principio de Sustitución de Liskov (Liskov Substitution Principle) establece que los objetos de una subclase deben poder sustituir a los de su superclase sin alterar el comportamiento correcto del sistema.

En el diseño orientado a objetos, esto implica que las subclases deben respetar el mismo contrato que define la clase base, asegurando que la jerarquía sea coherente y predecible.

### Este principio es esencial porque:

- Garantiza jerarquías de herencia correctas y estables.
- Evita comportamientos inesperados al usar polimorfismo.
- Permite que el sistema crezca sin romper su estructura.
- Mejora la mantenibilidad y extensibilidad del software.

Cuando se viola LSP, el código que usa una clase base ya no puede confiar en que las subclases se comporten correctamente, lo que genera validaciones adicionales y comportamientos condicionales no deseados.

---

## Motivación

En el sistema de gestión de proyectos audiovisuales del diseño de diagramas de clases inicial, hay múltiples jerarquías posibles: `Notificacion`, `Usuario`, `Proyecto`, entre otras.

Para mantener un diseño limpio y predecible, estas jerarquías deben cumplir LSP, garantizando que una subclase siempre pueda reemplazar a su clase base sin alterar el funcionamiento del sistema.

---

## Caso 1: Jerarquía de Notificaciones

### Problema identificado:
La clase `Notificacion` maneja distintos tipos de comunicación (email, SMS, interna). Si cada tipo se implementa con comportamientos incompatibles, se rompe LSP.

### Ejemplo de violación conceptual:
Una subclase `NotificacionSMS` que solo funcione si el destinatario tiene número cargado y, en caso contrario, genere un error.

### Consecuencias:

- Se necesitarían verificaciones del tipo de notificación antes de enviar.
- Se pierde el polimorfismo y se multiplica la lógica condicional.
- El código se vuelve más frágil y dependiente de los detalles de implementación.

### Diseño correcto:
Cada tipo de notificación (`NotificacionEmail`, `NotificacionInterna`, `NotificacionSMS`) debe respetar el método `enviar()` sin generar errores inesperados. Si un envío no es posible, simplemente no se realiza, pero no se rompe el contrato.

---

## Caso 2: Jerarquía de Usuarios por Rol

### Problema identificado:
La clase `Usuario` podría extenderse en diferentes roles: `ResponsableGeneral`, `ResponsableEtapa`, `Cliente`.

Una mala implementación sería eliminar o restringir métodos como `autenticar()` o `gestionarProyectos()` en alguna subclase.

### Diseño correcto:
Cada subclase define cómo responde a los métodos heredados, pero no si los tiene o no. Por ejemplo, `ResponsableEtapa` puede tener permisos limitados, pero sigue respondiendo al mismo contrato que `Usuario`.

---

## Caso 3: Jerarquía de Proyectos por Tipo

### Escenario:
`Proyecto` es la clase base. Subclases posibles: `ProyectoComercial`, `ProyectoDocumental`, `ProyectoInstitucional`.

### Violación típica:
Redefinir `consultarProyectosActivos()` para devolver un formato diferente o requerir parámetros adicionales.

### Diseño correcto:
Todas las subclases deben mantener la estructura y comportamiento del contrato definido por `Proyecto`.

---

## Explicación de Herencia

### ¿Qué es la Herencia?

La herencia permite crear nuevas clases basadas en otras, reutilizando atributos y comportamientos comunes. Las subclases pueden:

- Heredar comportamiento sin modificarlo.
- Especializar métodos para un caso particular.
- Extender con nuevos atributos o funcionalidades.

### Relación “ES-UN” (IS-A)

- Una `NotificacionEmail` es una `Notificacion`.
- Un `ResponsableEtapa` es un `Usuario`.
- Un `ProyectoComercial` es un `Proyecto`.

Mientras estas relaciones sean verdaderas sin contradicciones, el modelo respeta LSP.

---

## Aplicación de LSP en el Sistema

Para cumplir con LSP:

- **Precondiciones no más estrictas**: las subclases no deben exigir más que la clase base.
- **Postcondiciones no más débiles**: deben garantizar los mismos resultados esperados.
- **Invariantes preservadas**: las reglas del modelo se mantienen en todas las subclases.
- **Coherencia del contrato**: ningún método cambia su propósito o tipo de resultado.

### Ejemplo:
El método `enviar()` de `Notificacion` define el flujo general. Cada subclase lo implementa garantizando que el envío se realice o se registre correctamente.

---

## Estructura de Clases

![Diagrama de clases que aplica LSP](/diagramas\01-diagrama-clases\01-solid-03-lsp.png)

---

## Justificación Técnica

### Jerarquía 1: Sistema de Notificaciones (Cumple LSP)

- **Clase base**: `Notificacion`
- **Atributos**: `mensaje`, `fechaEnvio`, `tipo`
- **Método principal**: `enviar()`
- **Subclases**:
  - `NotificacionEmail`
  - `NotificacionInterna`
  - `NotificacionSMS`

**Cumplimiento**:

- Todas comparten el método `enviar()` con el mismo contrato.
- Si un envío no es posible, se maneja internamente.
- El sistema puede tratarlas indistintamente como `Notificacion`.

---

### Jerarquía 2: Usuarios por Rol (Cumple LSP)

- **Clase base**: `Usuario`
- **Atributos**: `nombre`, `rol`
- **Métodos**: `autenticar()`
- **Subclases**:
  - `ResponsableGeneral`
  - `ResponsableEtapa`
  - `Cliente`

**Cumplimiento**:

- Todas las subclases mantienen el método `autenticar()`.
- Los permisos se gestionan mediante composición o validaciones.
- El sistema puede usar cualquier tipo de `Usuario`.

---

### Jerarquía 3: Proyectos por Tipo (Cumple LSP)

- **Clase base**: `Proyecto`
- **Atributos**: `nombre`, `tipo`, `fechaInicio`, `fechaFin`, `responsableGeneral`
- **Métodos**: `crearProyecto()`, `consultarProyectosActivos()`
- **Subclases**:
  - `ProyectoComercial`
  - `ProyectoDocumental`
  - `ProyectoInstitucional`

**Cumplimiento**:

- Todas las subclases conservan los mismos métodos.
- Los resultados son coherentes con la clase base.
- El sistema puede procesar proyectos sin distinguir su tipo.

---

## Relaciones en el Diagrama

- **Herencia** (flecha con triángulo vacío): representa la relación “ES-UN”.
- **Métodos comunes**: se heredan y pueden ser extendidos o especializados.
- **Clases abstractas** (si las hubiera): definen contratos comunes que las subclases deben cumplir.