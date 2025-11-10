# Matriz CLAE (CRUD) – [Crear proyecto]

**Proyecto:** Sistema de Gestión de Proyectos Audiovisuales  
**Caso de Uso:** [CU1 - Crear proyecto]  

---

## 1) Tabla CLAE

> **Estructura:**  
> - **Filas:** Actividades internas del caso de uso (acciones o pasos del flujo).  
> - **Columnas:** Clases del sistema involucradas.  
> - **Celdas:** Letras **C**, **L**, **A**, **E** según la operación que se realiza sobre la clase.  
> - Si no aplica, dejar la celda vacía.  

| Actividad / Proyecto | Etapa | Usuario | Cliente | TipoDeProyecto | Notificación | FechaProyecto |
|--------------------|:--------:|:-----:|:-------:|:-----------------:|:-------------:|-----:|
| Crear proyecto | C |   | L |   |   |  |  |   |
| Definir Etapas | L | C |   |   |   |  |  |   |
| Nombrar responsable etapa | L | A | L |   |   |  |   |   |
| Definir tipo de proyecto | A |   |   |  | L |  | |   |
| Agregar observaciones iniciales | A |   |   |   |  |  |  |   |
| Validar informacion del proyecto | L |  L | L |   | A | L |  |   |
| Ingresar fechas (inico/fin) | L |  |  |   |  | C |   |   |
| Asociar clientes | A |   |   | L  |  |  |  |   |
| Enviar notificaciones| L | L |   |   |  | C | |  

> **Leyenda:**  
> **C**: Crear – **L**: Leer/Listar – **A**: Actualizar – **E**: Eliminar  

---

## 2) Métodos identificados

> Los métodos se derivan directamente de las operaciones (C/L/A/E) marcadas en la tabla.  
> Cada método deberá existir en la clase correspondiente del **diagrama de clases**, y reflejarse en su **Tarjeta CRC** y en el **diagrama de secuencia** del caso de uso.

| Clase | Método | Tipo (C/L/A/E) | Parámetros (nombre: tipo) | Retorno | Actividad asociada |
|--------|---------|----------------|----------------------------|----------|--------------------|
| Proyecto | `crearProyecto(nombre: string, descripcion: string)` | C | `nombre: string`, `descripcion: string` | `Proyecto` | Crear nuevo proyecto |
| Usuario | `gestionarUsuarios(idUsuario: int)` | L | `idUsuario: int` | `Usuario` | Crear nuevo proyecto |
| Proyecto | `buscarEtapas(descripcion: string)` | L | `descripcion: string` | `Proyecto` | Definir etapas |
| Etapa | `crearEtapas(idProyecto: int, descripcion: string)` | C | `idProyecto: int`, `descripcion: string` | `Etapa` | Definir etapas |
| Proyecto | `asignarResponsable (idEtapa: int, idUsuario: int)` | L | `proyectoId: int`, `archivo: File` | `int` | Nombrar responsable etapa |
| Etapa | `actualizarEtapas(idEtapas: int, descripcion: string)` | A | `idEtapa: int, idescripcion: string` | `etapa` | Nombrar responsable etapa |
| Usuario | `listarEtapas(idEtapas: int)` | L | `idEtapa: int, idescripcion: string` | `etapa` | Nombrar responsable etapa |
| Proyecto | `aagregarObservaciones (idProyecto: int, descripcion: string)` | A | `idProyecto: int, descripcion: string)` | `int` | Agregar observaciones iniciales|
| Proyecto | `validar (idProyectProyectoo: int)` | L | `idProyecto: int)` | `int` | Validar informacion del proyecto|
| Proyecto | `regstrarFechas (idProyecto: int, fechaInicio: date, fechaFin:date)` | L | `idProyecto: int, fechaInicio: date, fechaFin:date` | `int` | Ingresar fechas |
| Proyecto | `buscarCliente` | L |  |  | Asociar clientes |
| Notificacion | `crearNotificacion(idDestinatario: int, mensaje: string)` | C | dDestinatario: int, mensaje: string |  | Asociar clientes |



---

## 3) Relación con otros artefactos del diseño

> Esta sección documenta la **trazabilidad** del caso de uso con los demás artefactos del modelo.  
> Cada fila establece una correspondencia entre los elementos de la matriz CLAE y los artefactos donde aparecen.

| Elemento | Artefacto vinculado | Archivo / Referencia URL | Descripción de la relación |
|-----------|--------------------|-----------------------|-----------------------------|
| `crearProyecto()` | Tarjeta CRC – Proyecto | [`herramientas-agile/tarjetas-crc/crc-02-tarjeta-crc-proyecto.md`]() | Figura como responsabilidad “Crear proyecto”. |
| `crearProyecto()` | Diagrama de Secuencia – CU1 | [`diagramas/05-diagramas-secuencia/05-secuencia-creacion-proyecto-creacion-proyecto-exitoso-01.puml`]() | Aparece como mensaje enviado desde el actor “Productor” al objeto e `interfazWeb` |
| `crearProyecto()` | Diagrama de Actividad – CU1 | [`diagramas/04-diagramas-actividades/04-actividad-crear-proyecto-caso-uso-01.puml`]() | Acción “Seleccionar la opcion regristrar proyecto” coincide con la operación **C**. |

| `gestionarUsuarios()` | Tarjeta CRC – Sistema | [`herramientas-agile/tarjetas-crc/01-tarjeta-crc-sistema.md`]() | Figura como responsabilidad "gestionarUsuarios" |
| `gestionarUsuarios()` | Diagrama de Secuencia – CU1 | [`05-secuencia-consulta-proyectos-activos-consulta-exitosa-de-proyectos-activos-05.puml`]() | Se muestra como mensaje entre `interfazWeb` y `controlador`. |
| `gestionarUsuarios)` | Diagrama de Actividad – CU1|[`diagramas/04-diagramas-actividades/04-actividad-consultar-estadisticas-04.puml`] () | accion "autenticar usuario" coincide con la operacion **L**.|

| `buscarEtapas()` | Tarjeta CRC – Sistema | [`herramientas-agile/tarjetas-crc/02-tarjeta-crc-proyecto.md`]() | Figura como responsabilidad "gestionarEtapas" |
| `buscarEtapas()` | Diagrama de Secuencia – CU1 | [`05-secuencia-actualizar-estado-de-la-etapa-actualizacion-exitosa-del-estado-de-la-etapa-02.puml`]() | Se muestra como mensaje entre `servicioDeEtapa` y `baseDeDatos`. |
| `buscarEtapas()` | Diagrama de Actividad – CU1|[`diagramas/04-actividad-actualizar-estado-caso-uso-02.puml`] () | accion "seleccionar etapa asignada" coincide con la operacion **L**.|

| `crearEtapas()` | Tarjeta CRC – Sistema | [`herramientas-agile/tarjetas-crc/02-tarjeta-crc-proyecto.md`]() | Figura como responsabilidad "gestionarEtapas" |
| `crearEtapas()` | Diagrama de Secuencia – CU1 | [`05-secuencia-actualizar-estado-de-la-etapa-actualizacion-exitosa-del-estado-de-la-etapa-02.puml`]() | Se muestra como mensaje entre `servicioDeEtapa` y `baseDeDatos`. |
| `crearEtapas()` | Diagrama de Actividad – CU1|[`diagramas/04-actividad-actualizar-estado-caso-uso-02.puml`] () | accion "seleccionar etapa asignada" coincide con la operacion **L**.|

---

## 4) Issues e inconsistencias detectadas

> Registrar cualquier diferencia encontrada entre esta matriz y los artefactos relacionados.

| URL | Descripción de la inconsistencia | Artefacto relacionado | Acción correctiva | Estado |
|----|----------------------------------|------------------------|-------------------|:------:|
| [#82](https://github.com/9919-Mili/SistemaProductoraVideos/issues/82) | `crearEtapa()` no figura en la CRC de Etapa | Tarjeta CRC – Etapa | Agregar responsabilidad y actualizar CRC | Pendiente |
| [#46](https://github.com/tu-org/tu-repo/issues/46) | Acción “Notificar creación” no aparece en el diagrama de secuencia | Diagrama de Secuencia – CU1 | Incorporar mensaje a `Notificación` | Pendiente |
| [#46](https://github.com/tu-org/tu-repo/issues/45)| Método `subirArchivo()` sin tipo de retorno en diagrama de clases | Diagrama de Clases | Agregar tipo `bool` en puml | Resuelto |

**Estados posibles:** Abierto / Pendiente / Resuelto

---
