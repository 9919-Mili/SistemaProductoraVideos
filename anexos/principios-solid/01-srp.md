# Principio de Responsabilidad Única (SRP)

## Propósito y Tipo del Principio SOLID

El Principio de Responsabilidad Única (Single Responsibility Principle) establece que **una clase debe tener una única razón para cambiar**, es decir, debe tener una sola responsabilidad bien definida. Este principio es fundamental en el diseño orientado a objetos porque:

- Reduce el acoplamiento entre componentes del sistema
- Facilita el mantenimiento y la evolución del código
- Mejora la testabilidad al poder probar cada responsabilidad de forma aislada
- Aumenta la cohesión dentro de cada clase
- Minimiza el impacto de los cambios en el sistema

Cuando una clase tiene múltiples responsabilidades, los cambios en una de ellas pueden afectar o romper las otras, generando código frágil y difícil de mantener.

## Motivación

En el diseño inicial del sistema de gestión de proyectos de la productora de videos, se identificaron tres clases que violan claramente el Principio de Responsabilidad Única:

### Clase `Sistema`: El "God Object"

La clase `Sistema` concentraba cinco responsabilidades completamente diferentes:
- Gestión de proyectos
- Gestión de usuarios
- Generación de reportes estadísticos
- Envío de notificaciones
- Autenticación de usuarios

**Problema concreto:** Si necesitamos cambiar la lógica de envío de notificaciones (por ejemplo, agregar soporte para WhatsApp además de email), debemos modificar la clase `Sistema`, que también maneja la autenticación y la gestión de proyectos. Esto genera:
- Alto riesgo de introducir bugs en funcionalidades no relacionadas
- Dificultad para testear cada responsabilidad de forma aislada
- Código altamente acoplado y difícil de mantener
- Imposibilidad de reutilizar componentes de forma independiente

### Clase `Proyecto`: Mezcla de Modelo y Repositorio

La clase `Proyecto` mezclaba dos responsabilidades:
- Representar el modelo de datos de un proyecto (atributos y comportamiento)
- Consultar proyectos en el sistema (`consultarProyectosActivos()`)

**Problema concreto:** Si cambiamos la estrategia de persistencia (de base de datos relacional a NoSQL, por ejemplo), debemos modificar la clase que representa el modelo de dominio. Esto viola la separación de concerns y hace que el modelo esté acoplado a la capa de acceso a datos.

### Clase `Etapa`: Múltiples Gestiones

La clase `Etapa` gestionaba tres aspectos diferentes:
- Estado y datos propios de la etapa
- Colección de comentarios
- Colección de adjuntos

**Problema concreto:** Si necesitamos implementar búsqueda avanzada de comentarios o validación específica para adjuntos, debemos modificar la clase `Etapa`, generando una clase cada vez más compleja y difícil de mantener.

## Estructura de Clases

![Diagrama SRP](/SistemaProductoraVideos/anexos/principios-solid/01-solid-01-srp.png)

[Ver diagrama en detalle](/SistemaProductoraVideos/anexos/principios-solid/01-solid-01-srp.puml)

## Justificación Técnica

### Refactorización 1: Descomposición de la clase `Sistema`

#### Antes (violaba SRP):
Sistema

gestionarProyectos()
gestionarUsuarios()
generarReportes()
notificarUsuarios()
accesoAutenticado()


#### Después (cumple SRP):

**1. `GestorProyectos`**
- Responsabilidad única: Gestión del ciclo de vida de proyectos
- Métodos: crearProyecto(), actualizarProyecto(), eliminarProyecto()
- Razón única para cambiar: cambios en la lógica de negocio de proyectos

**2. `GestorUsuarios`**
- Responsabilidad única: Gestión de usuarios del sistema
- Métodos: crearUsuario(), actualizarUsuario(), asignarRol()
- Razón única para cambiar: cambios en la gestión de usuarios

**3. `GeneradorReportes`**
- Responsabilidad única: Generación de reportes y estadísticas
- Métodos: generarReporteProyectos(), generarEstadisticas()
- Razón única para cambiar: cambios en tipos de reportes o formatos

**4. `ServicioNotificaciones`**
- Responsabilidad única: Envío de notificaciones
- Métodos: notificarPorEmail(), notificarPorWhatsApp()
- Razón única para cambiar: cambios en canales o estrategias de notificación

**5. `ServicioAutenticacion`**
- Responsabilidad única: Autenticación y autorización
- Métodos: autenticar(), validarPermisos()
- Razón única para cambiar: cambios en mecanismos de seguridad

### Refactorización 2: Separación de `Proyecto` y `RepositorioProyectos`

#### Antes (violaba SRP):
Proyecto

atributos del proyecto


crearProyecto()
consultarProyectosActivos()  // Responsabilidad de acceso a datos


#### Después (cumple SRP):

**1. `Proyecto`** (Modelo de dominio)
- Responsabilidad única: Representar un proyecto con su lógica de negocio
- Atributos: nombre, tipo, fechas, etapas, responsable
- Métodos: validarFechas(), agregarEtapa(), calcularProgreso()
- Razón única para cambiar: cambios en la estructura o reglas de negocio del proyecto

**2. `RepositorioProyectos`** (Capa de acceso a datos)
- Responsabilidad única: Persistencia y consulta de proyectos
- Métodos: guardar(), actualizar(), consultarProyectosActivos(), buscarPorId()
- Razón única para cambiar: cambios en la estrategia de persistencia

**Relación:** `RepositorioProyectos` depende de `Proyecto` (dependencia), pero `Proyecto` no conoce al repositorio, manteniendo el modelo de dominio limpio.

### Refactorización 3: Descomposición de la clase `Etapa`

#### Antes (violaba SRP):
Etapa

atributos de etapa
comentarios: List<Comentario>
adjuntos: List<Adjunto>


actualizarEstado()


#### Después (cumple SRP):

**1. `Etapa`** (Modelo de dominio)
- Responsabilidad única: Gestionar el estado y comportamiento de una etapa
- Atributos: nombre, estado, fechas, responsable
- Métodos: actualizarEstado(), validarTransicion(), calcularProgreso()
- Razón única para cambiar: cambios en la lógica de estados de etapa

**2. `GestorComentarios`**
- Responsabilidad única: Gestión de comentarios de una etapa
- Métodos: agregarComentario(), eliminarComentario(), buscarComentarios()
- Razón única para cambiar: cambios en la lógica de gestión de comentarios

**3. `GestorAdjuntos`**
- Responsabilidad única: Gestión de archivos adjuntos de una etapa
- Métodos: agregarAdjunto(), eliminarAdjunto(), descargarAdjunto(), validarFormato()
- Razón única para cambiar: cambios en la gestión de archivos o validaciones

**Relaciones:** 
- `Etapa` tiene una relación de composición con `GestorComentarios` y `GestorAdjuntos`
- Cada gestor maneja su propia colección de forma independiente

## Beneficios de la Refactorización

### Mantenibilidad
Cada clase es más pequeña, enfocada y fácil de entender. Los cambios en una responsabilidad no afectan a las demás.

### Testabilidad
Podemos crear tests unitarios específicos para cada responsabilidad sin necesidad de mockear componentes no relacionados.

### Reutilización
Los servicios (`ServicioNotificaciones`, `RepositorioProyectos`, etc.) pueden ser reutilizados en otros contextos del sistema.

### Extensibilidad
Agregar nuevas funcionalidades (como un nuevo canal de notificación) requiere extender solo la clase correspondiente, sin tocar otras partes del sistema.

### Cohesión
Cada clase tiene alta cohesión: todos sus métodos trabajan sobre datos relacionados y tienen un propósito común.