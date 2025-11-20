# Matriz CLAE (CRUD) – [Agregar observaciones]

**Proyecto:** Sistema de Gestión de Proyectos Audiovisuales  
**Caso de Uso:** [CU3 - Agregar observaciones]  

---

## 1) Tabla CLAE

> **Estructura:**  
> - **Filas:** Actividades internas del caso de uso (acciones o pasos del flujo).  
> - **Columnas:** Clases del sistema involucradas.  
> - **Celdas:** Letras **C**, **L**, **A**, **E** según la operación que se realiza sobre la clase.  
> - Si no aplica, dejar la celda vacía.  

| Actividad / Clase | Proyecto | Etapa | Usuario | Observaciones | Notificación |
|--------------------|:--------:|:-----:|:-------:|:-----------------:|:-------------:|-----:|
| Seleccionar proyecto | L |   | L |   |   |  
| Verificar permisos | L |  | L |   |   |  
| Seleccionar etapa | L | L |  |   |   |  
| Mencionar usuario |  |   | L |  |   |  
| Adjuntar archivos | L |   |   |   |  |  
| Escribir Observacion | L | L |   | C |  | 
| Elegir tipo de observacion | L |   |   | A |  |  
| Confirmar observacion | L | L |   | A  |  |  
| Enviar notificaciones | |   |  L |   | C |  


> **Leyenda:**  
> **C**: Crear – **L**: Leer/Listar – **A**: Actualizar – **E**: Eliminar  

---

## 2) Métodos identificados

> Los métodos se derivan directamente de las operaciones (C/L/A/E) marcadas en la tabla.  
> Cada método deberá existir en la clase correspondiente del **diagrama de clases**, y reflejarse en su **Tarjeta CRC** y en el **diagrama de secuencia** del caso de uso.

| Clase | Método | Tipo (C/L/A/E) | Parámetros (nombre: tipo) | Retorno | Actividad asociada |
|--------|---------|----------------|----------------------------|----------|--------------------|
| Proyecto | `listarProyecto(nombre: string, fechaInicio: date)` | L | `nombre: string`, `fechaInicio: date` | `Proyecto` | Listar proyecto |
| Etapa | `listarEtapa(proyectoId: int, nombre: string)` | L | `proyectoId: int`, `nombre: string` | `Etapa` | Listar etapa del proyecto |
| Usuario | `seleccionarUsuario(id: int, usuarioId: int)` | L | `id: int`, `usuarioId: int` | `Usuario` | Buscar usuario |
| Observaciones | `crearObservacion(proyectoId: int, etapaId: int, observacion: date)` | C | `proyectoId: int, etapaId: int, observacion: string` | `Observaciones` | Crear una observacion |
| Notificación | `crearNotificacion(proyectoId: int, mensaje: string)` | C | `proyectoId: int`, `mensaje: string` | `Notificacion` | Enviar notificacion |

---

## 3) Relación con otros artefactos del diseño

> Esta sección documenta la **trazabilidad** del caso de uso con los demás artefactos del modelo.  
> Cada fila establece una correspondencia entre los elementos de la matriz CLAE y los artefactos donde aparecen.

| Elemento | Artefacto vinculado | Archivo / Referencia URL | Descripción de la relación |
|-----------|--------------------|-----------------------|-----------------------------|
| `listarProyecto()` | Tarjeta CRC – Sistema | [`herramientas-agile/tarjetas-crc/01-tarjeta-crc-sistema.md`]() | Figura como responsabilidad “Gestionar proyectos”. |
| `listarProyecto()` | Diagrama de Secuencia – CU3 | [`diagramas/05-diagramas-secuencia/05-secuencia-consulta-proyectos-activos-consulta-exitosa-de-proyectos-activos-05.puml`]() | Aparece como mensaje enviado dessde `Controlador` al objeto `servicioProyecto`. |
| `listarProyecto()` | Diagrama de Actividad – CU3 | [`diagramas/04-diagramas-actividades/04-actividad-actualizar-estado-caso-uso-02.png`]() | "Seleccionar proyecto correspondiente” coincide con la operación **L**. |
| `listarEtapa()` | Tarjeta CRC – Proyecto | [`herramientas-agile/tarjetas-crc/02-tarjeta-crc-proyecto.md`]() | Figura como responsabilid "Gestionar etapas". |
| `listarEtapa()` | Diagrama de Secuencia – CU3 | [`diagramas/05-diagramas-secuencia/05-secuencia-actualizar-estado-de-la-etapa-actualizacion-exitosa-del-estado-de-la-etapa-02.puml`]() | Se muestra como mensaje entre `servicioDeEtapa` y `baseDeDatos`. |
| `listarEtapa()` | Diagrama de Actividad – CU3 | [`diagramas/04-diagramas-actividades/04-actividad-agregar-observaciones-03.puml`]() | "Seleccionar una etapa" coincide con la operacion **L**. |
| `seleccionarUsuario()` | Tarjeta CRC – Sistema | [`herramientas-agile/tarjetas-crc/01-tarjeta-crc-sistema.md`]() | Figura como responsabilid "Gestionar usuarios". |
| `seleccionarUsuario()` | Diagrama de Secuencia – CU3 | [`diagramas/05-diagramas-secuencia/05-secuencia-consulta-proyectos-activos-consulta-exitosa-de-proyectos-activos-05.puml`]() | Se muestra como mensaje entre `usuarioAutorizado` y `controlador`. |
| `seleccionarUsuario()` | Diagrama de Actividad – CU3 | [`diagramas/04-diagramas-actividades/04-actividad-consultar-proyectos-activos-05.puml`]() | "Autenticar usuario" coincide con la operacion **L**. |
| `crearComentario()` | Tarjeta CRC – Observacion | [`herramientas-agile/tarjetas-crc/08-tarjeta-crc-observacion.md`]() | Figura como responsabilid "Agregar comentario". |
| `crearComentario()` | Diagrama de Secuencia – CU3 | [`diagramas/05-diagramas-secuencia/05-secuencia-agregar-observaciones-agregado-exitoso-de-observaciones-03.puml`]() | Se muestra como mensaje entre `usuarioAutorizado` y `interfazSistema`. |
| `crearComentario()` | Diagrama de Actividad – CU3 | [`diagramas/04-diagramas-actividades/04-actividad-agregar-observaciones-03.puml`]() | "Escribir comentario" coincide con la operacion **C**. |
| `crearNotificacion()` | Tarjeta CRC – Notificacion | [`herramientas-agile/tarjetas-crc/05-tarjeta-crc-notificacion.md`]() | Figura como responsabilid "Enviar aviso al usuario". |
| `crearNotificacion()` | Diagrama de Secuencia – CU3 | [`diagramas/05-diagramas-secuencia/05-secuencia-consulta-estadisticas-consulta-automatica-mensual-de-estadisticas-04.puml.`]() | Se muestra como mensaje entre `controlador` y `sistema`. |
| `crearNotificacion()` | Diagrama de Actividad – CU3 | [`diagramas/04-diagramas-actividades/04-actividad-actualizar-estado-caso-uso-02.puml`]() | "Enviar notificacion de cambio de estado" coincide con la operacion **C**. |
---

## 4) Issues e inconsistencias detectadas

> Registrar cualquier diferencia encontrada entre esta matriz y los artefactos relacionados.

| URL | Descripción de la inconsistencia | Artefacto relacionado | Acción correctiva | Estado |
|----|----------------------------------|------------------------|-------------------|:------:|
| [#89](https://github.com/9919-Mili/SistemaProductoraVideos/issues/89) | Acción “seleccionarUsuario” no aparece en el diagrama de secuencia | Diagrama de Secuencia – CU3 | Incorporar mensaje a `usuarioAutorizado` |Resuelto |


**Estados posibles:** Abierto / Pendiente / Resuelto

---
