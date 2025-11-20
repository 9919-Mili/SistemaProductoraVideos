# Matriz CLAE (CRUD) – [Crear proyecto]

**Proyecto:** Sistema de Gestión de Proyectos Audiovisuales  
**Caso de Uso:** [CU1 - Crear proyecto ]  

---

## 1) Tabla CLAE

> **Estructura:**  
> - **Filas:** Actividades internas del caso de uso (acciones o pasos del flujo).  
> - **Columnas:** Clases del sistema involucradas.  
> - **Celdas:** Letras **C**, **L**, **A**, **E** según la operación que se realiza sobre la clase.  
> - Si no aplica, dejar la celda vacía.  

| Actividad / Clase | Proyecto | Etapa | Usuario | Cliente | TipoDeProyecto | Notificación | FechaProyecto |
|--------------------|:--------:|:-----:|:-------:|:-----------------:|:-------------:|-----:|
| Crear proyecto | C |   | L |   |   |  | |
| Definir etapas | L | C |   |   |   |  | |
| Nombrar responsable etapa | L | A | L |   |  |  | |
| Definir tipo de proyecto | A |   |   |  | L |  | |
| Agregar observaciones iniciales | A |   |   |   |  |  | |
| Validar informacion del proyecto| L | L | L |  | A | L | |
| Ingresar fechas (inicio/fin) | L |   |   |   | C |  | |
| Asociar cliente | A |   |   | L |   |  | |
| Enviar notificacion | L | L |   |   |  | C | |

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
| Proyecto | `agregarObservaciones (idProyecto: int, descripcion: string)` | A | `idProyecto: int, descripcion: string)` | `int` | Agregar observaciones iniciales|
| Proyecto | `validarInformacion (idProyectProyectoo: int)` | L | `idProyecto: int)` | `int` | Validar informacion del proyecto|
| Proyecto | `registrarFechas (idProyecto: int, fechaInicio: date, fechaFin:date)` | L | `idProyecto: int, fechaInicio: date, fechaFin:date` | `int` | Ingresar fechas |
| Proyecto | `buscarCliente` | L |  |  | Asociar clientes |
| Notificacion | `crearNotificacion(idDestinatario: int, mensaje: string)` | C | `idDestinatario: int, mensaje: string` |  | Asociar clientes |



---

## 3) Relación con otros artefactos del diseño

> Esta sección documenta la **trazabilidad** del caso de uso con los demás artefactos del modelo.  
> Cada fila establece una correspondencia entre los elementos de la matriz CLAE y los artefactos donde aparecen.

| Elemento | Artefacto vinculado | Archivo / Referencia URL | Descripción de la relación |
|-----------|--------------------|-----------------------|-----------------------------|
| `crearProyecto()` | Tarjeta CRC – Proyecto | [`herramientas-agile/tarjetas-crc/02-tarjeta-crc-proyecto.md`]() | Figura como responsabilidad “Crear proyecto”. |
| `crearProyecto()` | Diagrama de Secuencia – CU1 | [`diagramas/05-diagramas-secuencia/05-secuencia-creacion-proyecto-creacion-proyecto-exitoso-01.puml`]() | Aparece como mensaje enviado desde el actor “Productor” al objeto `interfazWeb` |
| `crearProyecto()` | Diagrama de Actividad – CU1 |[`diagramas/04-diagramas-actividades/04-actividad-crear-proyecto-caso-uso-01.puml`]() | Acción “Seleccionar la opcion regristrar proyecto” coincide con la operación **C**. |
| `gestionarUsuarios()` | Tarjeta CRC – Sistema | [`herramientas-agile/tarjetas-crc/01-tarjeta-crc-sistema.md`]() | Figura como responsabilidad "gestionarUsuarios" |
| `gestionarUsuarios()` | Diagrama de Secuencia – CU1 | [`diagramas/05-diagramas-secuencia/05-secuencia-consulta-proyectos-activos-consulta-exitosa-de-proyectos-activos-05.puml`]() | Se muestra como mensaje entre `interfazWeb` y `controlador`. |
| `gestionarUsuarios()` | Diagrama de Actividad – CU1|[`diagramas/04-diagramas-actividades/04-actividad-consultar-estadisticas-04.puml`]() | accion "autenticar usuario" coincide con la operacion **L**.|
| `crearEtapas()` | Tarjeta CRC – Etapa| [herramientas-agile/tarjetas-crc/03-tarjeta-crc-etapa.md]() | Figura como responsabilidad "Crear etapa"  |
| `crearEtapas()` | Diagrama de Secuencia – CU1 | [diagramas/05-diagramas-secuencia/05-secuencia-actualizar-estado-de-la-etapa-actualizacion-exitosa-del-estado-de-la-etapa-02.png]() | Se muestra como mensaje entre `interfazDelSistema` y `responsableEtapa`|
| `crearEtapas()` | Diagrama de Actividad – CU1| | |
| `asignarResponsables()` | Tarjeta CRC – Etapa | [`herramientas-agile/tarjetas-crc/03-tarjeta-crc-etapa.md`]() | Figura como responsabilidad "Asignar responsable etapa" |
| `asignarResponsables()` | Diagrama de Secuencia – CU1 | [`diagramas/05-diagramas-secuencia/05-secuencia-agregar-observaciones-agregado-exitoso-de-observaciones-03.puml`]() | |
| `asignarResponsables()` | Diagrama de Actividad – CU1| [diagramas/04-diagramas-actividades/04-actividad-actualizar-estado-caso-uso-02.png]() | accion "Registrar responsable que actualiza" **A**|
| `actualizarEtapas()` | Tarjeta CRC – Etapa | [`herramientas-agile/tarjetas-crc/03-tarjeta-crc-etapa.md`]() | Figura como responsabilidad "Actualizar Estado" |
| `actualizarEtapas()` | Diagrama de Secuencia – CU1 | [`diagramas/05-diagramas-secuencia/05-secuencia-actualizar-estado-de-la-etapa-actualizacion-exitosa-del-estado-de-la-etapa-02.puml`]() | Se muestra como mensaje entre `controlador` y `baseDeDatos`. |
| `actualizarEtapas()` | Diagrama de Actividad – CU1|[`diagramas/05-diagramas-secuencia/05-secuencia-actualizar-estado-de-la-etapa-actualizacion-exitosa-del-estado-de-la-etapa-02.puml`]() | accion "confirmar cambio de estado" **A**.|
| `listarEtapas()` | Tarjeta CRC – Etapa | [`herramientas-agile/tarjetas-crc/03-tarjeta-crc-etapa.md`]() | Figura como responsabilidad "Consultar en que etapa estan trabajando" |
| `listarEtapas()` | Diagrama de Secuencia – CU1 | [`ddiagramas/05-diagramas-secuencia/05-secuencia-actualizar-estado-de-la-etapa-actualizacion-exitosa-del-estado-de-la-etapa-02.puml`]() | Se muestra como mensaje entre `servicioDeEtapa` y `baseDeDatos`. |
| `listarEtapas()` | Diagrama de Actividad – CU1|[`ddiagramas/05-diagramas-secuencia/05-secuencia-agregar-observaciones-agregado-exitoso-de-observaciones-03.puml`]() | accion "Mostrar detalles de etapas" **L**.|
| `agregarObservaciones()` | Tarjeta CRC – Observacion | [`herramientas-agile/tarjetas-crc/08-tarjeta-crc-observacion.md`]() | Figura como responsabilidad "Agregar comentario" |
| `agregarObservaciones()` | Diagrama de Secuencia – CU1 | [`diagramas/05-diagramas-secuencia/05-secuencia-agregar-observaciones-agregado-exitoso-de-observaciones-03.puml`]() | Se muestra como mensaje entre `servicioComentario` y `baseDeDatos`. |
| `agregarObservaciones()` | Diagrama de Actividad – CU1|[`diagramas/04-diagramas-actividades/04-actividad-agregar-observaciones-03.puml`]() | accion "Escribir comentario" **A**.|
| `validarInformacion()` | Tarjeta CRC – Usuario | [`herramientas-agile/tarjetas-crc/04-tarjeta-crc-usuario.md`]() | Figura como responsabilidad "Validar datos" |
| `validarInformacion()` | Diagrama de Secuencia – CU1 | [`diagramas/05-diagramas-secuencia/05-secuencia-agregar-observaciones-agregado-exitoso-de-observaciones-03.puml`]() | Se muestra como mensaje entre `controlador` y `servicioDeComentario`. |
| `validarInformacion()` | Diagrama de Actividad – CU1|[`diagramas/04-diagramas-actividades/04-actividad-consultar-proyectos-activos-05.puml`]() | accion "Validar credenciales" **L**.|
| `registrarFechas()` | Tarjeta CRC – Observacion | [`herramientas-agile/tarjetas-crc/08-tarjeta-crc-observacion.md`]() | Figura como responsabilidad "Registrar fechas de cambios" |
| `registrarFechas()` | Diagrama de Secuencia – CU1 | [`diagramas/05-diagramas-secuencia/05-secuencia-actualizar-estado-de-la-etapa-actualizacion-exitosa-del-estado-de-la-etapa-02.puml`]() | Se muestra como mensaje entre `servicioDeEtapas` y `baseDeDatos`. |
| `registrarFechas()` | Diagrama de Actividad – CU1|[`diagramas/04-diagramas-actividades/04-actividad-actualizar-estado-caso-uso-02.puml`]() | accion "Registrar responsable que actualiza estado anterior, fecha/hora" **L**.|
| `buscarCliente()` | Tarjeta CRC – Proyecto| [`herramientas-agile/tarjetas-crc/02-tarjeta-crc-proyecto.md`]()| Figura como responsabilidad "buscar cliente" |
| `buscarCliente()` | Diagrama de Secuencia – CU1 | [`diagramas/05-diagramas-secuencia/05-secuencia-consulta-proyectos-activos-consulta-exitosa-de-proyectos-activos-05.png`]() | figura como mensaje entre `controlador` y `servicioProyectos` |
| `buscarCliente()` | Diagrama de Actividad – CU1|||
| `crearNotificacion()` | Tarjeta CRC – Notificacion | [`herramientas-agile/tarjetas-crc/05-tarjeta-crc-notificacion.md`]() | Figura como responsabilidad "Generar mensaje de retraso" |
| `crearNotificacion()` | Diagrama de Secuencia – CU1 | [`diagramas/05-diagramas-secuencia/05-secuencia-agregar-observaciones-agregado-exitoso-de-observaciones-03.puml`]() | Se muestra como mensaje entre `interfazSistema` y `usuarioAutorizado`. |
| `crearNotificacion()` | Diagrama de Actividad – CU1|[`diagramas/04-diagramas-actividades/04-actividad-agregar-observaciones-03.puml`]() | accion "Generar mensaje de notificacion" **C**.|
---



## 4) Issues e inconsistencias detectadas

> Registrar cualquier diferencia encontrada entre esta matriz y los artefactos relacionados.

| URL | Descripción de la inconsistencia | Artefacto relacionado | Acción correctiva | Estado |
|----|----------------------------------|------------------------|-------------------|:------:|
| [#82](https://github.com/9919-Mili/SistemaProductoraVideos/issues/82) | `crearEtapa()` no figura en la CRC de Etapa | Tarjeta CRC – Etapa | Agregue responsabilidad y actualice CRC | Resuelto |
| [#82](https://github.com/9919-Mili/SistemaProductoraVideos/issues/82) | Acción “Notificar cambio” no aparece en el diagrama de secuencia | Diagrama de Secuencia – CU1 | Incorporar mensaje a `responsableEtapa` | Resuelto |
| [#82](https://github.com/9919-Mili/SistemaProductoraVideos/issues/82)| Método `CrearEtapa()` sin tipo de retorno en diagrama de clases | Diagrama de Clases | Agregar tipo `bool` en puml | Pendiente |
| [#83](https://github.com/9919-Mili/SistemaProductoraVideos/issues/83#) | `asignarResponsables()` Accion "Asignar responsable de etapas" no aparece en el diagrama de secuencias - CU1 | Diagrama de Secuencia CU1 | agregue mensaje | Resuelto |
| [#83](https://github.com/9919-Mili/SistemaProductoraVideos/issues/83#)| Método `asignarResponsables()` sin tipo de retorno en diagrama de clases | Diagrama de Clases | Agregar tipo `bool` en puml | Resuelto |
| [#84](https://github.com/9919-Mili/SistemaProductoraVideos/issues/84) | `buscarCliente()` no figura en la CRC de Proyecto | Tarjeta CRC – Proyecto | Agregue responsabilidad y actualice CRC | Resuelto |
| [#84](https://github.com/9919-Mili/SistemaProductoraVideos/issues/84) | Acción “buscarCliente” no aparece en el diagrama de secuencia | Diagrama de Secuencia – CU1 | Incorporar mensaje a `baseDeDatos` | Resuelto |
| [#84](https://github.com/9919-Mili/SistemaProductoraVideos/issues/84)| Método `CrearEtapa()` sin tipo de retorno en diagrama de clases | Diagrama de Clases | Agregar tipo `bool` en puml | Pendiente

**Estados posibles:** Abierto / Pendiente / Resuelto

---
