# Matriz CLAE (CRUD) – [Actualizar estado etapa]

**Proyecto:** Sistema de Gestión de Proyectos Audiovisuales  
**Caso de Uso:** [CU2 - Actualizar estado etapa]  

---

## 1) Tabla CLAE

> **Estructura:**  
> - **Filas:** Actividades internas del caso de uso (acciones o pasos del flujo).  
> - **Columnas:** Clases del sistema involucradas.  
> - **Celdas:** Letras **C**, **L**, **A**, **E** según la operación que se realiza sobre la clase.  
> - Si no aplica, dejar la celda vacía.  

| Actividad / Clase | Proyecto | Etapa | Usuario | ArchivoMultimedia | Notificación | ... |
|--------------------|:--------:|:-----:|:-------:|:-----------------:|:-------------:|-----:|
| Seleccionar proyecto | L |   |  |   |   |  |
| Seleccionar etapa asiganada | L | L | L |   |   |  |
| Elegir nuevo estado |  | L |  |  |   |  |
| Agregar Observacion |  | L |  |  |  |  |
| Validar cambio de estado |  | A |   |  |  |  |
| Verificar permisos | L | L | L |  |   | |
| Validar transicion de estado |  | L |   |  |  |  |
| Validar requisitos del estado |  | L |  | |  |  |
| Actualizar estado de etapa | | A |   |  |  |  |
| Confirmar actualizacion |  | L |  | |   |  |
| Enviar notificacion | L | L | L |   |  | C |
| Identificar siguiente resposable | L | L | A |   |  |  |
| Notificar siguiente etapa |  | L | L |   |  | C |


> **Leyenda:**  
> **C**: Crear – **L**: Leer/Listar – **A**: Actualizar – **E**: Eliminar  

---

## 2) Métodos identificados

> Los métodos se derivan directamente de las operaciones (C/L/A/E) marcadas en la tabla.  
> Cada método deberá existir en la clase correspondiente del **diagrama de clases**, y reflejarse en su **Tarjeta CRC** y en el **diagrama de secuencia** del caso de uso.

| Clase | Método | Tipo (C/L/A/E) | Parámetros (nombre: tipo) | Retorno | Actividad asociada |
|--------|---------|----------------|----------------------------|----------|--------------------|
| Proyecto | `gestionarProyecto(nombre: string, fechaInicio: date)` | L | `nombre: string`, `fechaInicio: date` | `Proyecto` | Seleccionar proyecto |
| Etapa| `listarEtapas(etapasId: int, nombre: string)` | L | `etapasId: int`, `nombre: string` | `Etapa` | Listar etapas asignadas |
| Etapa | `actualizarEstado(idEtapas: int, nombre: string)` | A | `idEtapas: int, nombre: string` | `bool` | Validar cambio de estado |
| Usuario | `gestionarUsuario(nombre: string)` | L | `nombre: string` | `bool` | Verificar permisos |
| Notificación | `enviarNotificacion(proyectoId: int, mensaje: string)` | C | `proyectoId: int`, `mensaje: string` | `bool` | Notificar creación |
| Notificación | `NotificarSiguienteEtapa(proyectoId: int, mensaje: string)` | C | `proyectoId: int`, `mensaje: string` | `bool` | Notificar creación de siguiente etapa|

---

## 3) Relación con otros artefactos del diseño

> Esta sección documenta la **trazabilidad** del caso de uso con los demás artefactos del modelo.  
> Cada fila establece una correspondencia entre los elementos de la matriz CLAE y los artefactos donde aparecen.

| Elemento | Artefacto vinculado | Archivo / Referencia URL | Descripción de la relación |
|-----------|--------------------|-----------------------|-----------------------------|
| `gestionarProyecto()` | Tarjeta CRC – Proyecto | [`herramientas-agile/tarjetas-crc/01-tarjeta-crc-sistema.md`]() | Figura como responsabilidad “Gestionar proyectos”. |
| `gestionarProyecto()` | Diagrama de Secuencia – CU2 | [`diagramas/05-diagramas-secuencia/05-secuencia-crear-proyecto.puml`]() | Aparece como mensaje enviado desde el actor `interfazSistema` al objeto `controlador`. |
| `gestionarProyecto()` | Diagrama de Actividad – CU2 | [`diagramas/04-actividad-actualizar-estado-caso-uso-02.puml`]() | Acción “Seleccionar proyecto correspondiente” coincide con la operación **L**. |
| `listarEtapas()` | Tarjeta CRC – Proyecto| [`02-tarjeta-crc-proyecto.md`]() | Declarado como método dentro de las responsabilidades del proyecto. |
| `listarEtapas()` | Diagrama de Secuencia – CU2 | [`05-secuencia-agregar-observaciones-agregado-exitoso-de-observaciones-03.puml`]() | Se muestra como mensaje entre `servicioEtapa` y `baseDeDatos`. |
| `listarEtapas()` | Diagrama de Actividad – CU1 | [`04-actividad-actualizar-estado-caso-uso-02.puml`]() | Acción "Seleccionar etapa asignada" coincide con la operación **L** |
| `actualizarEstado()` | Tarjeta CRC – Proyecto| [`02-tarjeta-crc-proyecto.md`]() | Declarado como método dentro de las responsabilidades del proyecto. |
| `actualizarEstado()` | Diagrama de Secuencia – CU2 | [`05-secuencia-agregar-observaciones-agregado-exitoso-de-observaciones-03.puml`]() | Se muestra como mensaje entre `servicioEtapa` y `baseDeDatos`. |
| `actualizarEstado()` | Diagrama de Actividad – CU1 |[`04-actividad-actualizar-estado-caso-uso-02.puml`]() | Acción "Seleccionar etapa asignada" coincide con la operación **A** |
| `gestionarUsuario()` | Tarjeta CRC – Sistema| [`01-tarjeta-crc-sistema.md`]() | Declarado como método dentro de las responsabilidades del sistema. |
| `gestionarUsuario()` | Diagrama de Secuencia – CU2 | [`05-secuencia-consulta-proyectos-activos-consulta-exitosa-de-proyectos-activos-05.puml`]() | Se muestra como mensaje entre `usuarioAutorizado` y `interfazSistema`. |
| `gestionarUsuario()` | Diagrama de Actividad – CU1| [`04-actividad-consultar-estadisticas-04.puml`]() | Acción "Autenticar usuario" coincide con la operación **L** |
| `enviarNotificacion()` | Tarjeta CRC – Notificacion| [`05-tarjeta-crc-notificacion.md`]() | Declarado como método dentro de las responsabilidades de notificacion. |
| `enviarNotificacion()` | Diagrama de Secuencia – CU2 | [`05-secuencia-creacion-proyecto-creacion-proyecto-exitoso-01.puml`]() | Se muestra como mensaje entre `sistemaValidacion` y `interfazWeb`. |
| `enviarNotificacion()` | Diagrama de Actividad – CU2 | [`04-actividad-actualizar-estado-caso-uso-02.puml`]() | Acción "enviar notificacion de cambio de estado" coincide con la operación **C** |
| `notificarSigueinteEtapa()` | Tarjeta CRC – Notificacion| [`05-tarjeta-crc-notificacion.md`]() | Declarado como método dentro de las responsabilidades de Notificacion. |
| `notificarSigueinteEtapa()` | Diagrama de Secuencia – CU2 | [`05-secuencia-actualizar-estado-de-la-etapa-actualizacion-exitosa-del-estado-de-la-etapa-02`]() | Se muestra como mensaje entre `interfazDelsistema` y `responsableEtapa`. |
| `notificarSigueinteEtapa()` | Diagrama de Actividad – CU2|  [`04-actividad-actualizar-estado-caso-uso-02.puml`]() | Acción "Enviar notificacion cambio de estado" coincide con la operación **C** |



---

## 4) Issues e inconsistencias detectadas

> Registrar cualquier diferencia encontrada entre esta matriz y los artefactos relacionados.

| URL | Descripción de la inconsistencia | Artefacto relacionado | Acción correctiva | Estado |
|----|----------------------------------|------------------------|-------------------|:------:|
| [#85](https://github.com/9919-Mili/SistemaProductoraVideos/issues/85) | `notificarSiguenteEtapa()` no figura en la CRC de Notificacion | Tarjeta CRC – Notificacion | Agregar responsabilidad y actualizar CRC | Resuelto |


**Estados posibles:** Abierto / Pendiente / Resuelto

---
