# Matriz CLAE (CRUD) – Agregar Observaciones

**Proyecto:** Sistema Productora de Videos  
**Caso de Uso:** CU4 – Agregar Observaciones  

---

## 1) Tabla CLAE

> **Estructura:**  
> - **Filas:** Actividades internas del caso de uso (acciones o pasos del flujo).  
> - **Columnas:** Clases del sistema involucradas.  
> - **Celdas:** Letras **C**, **L**, **A**, **E** según la operación que se realiza sobre la clase.  
> - Si no aplica, dejar la celda vacía.  

| Actividad / Clase | Proyecto | Etapa | Usuario | Observación | Notificación | Reporte |
|--------------------|:--------:|:-----:|:-------:|:------------:|:-------------:|:-------:|
| Seleccionar proyecto activo | L |   | L |   |   |   |
| Elegir etapa correspondiente | L | L |   |   |   |   |
| Redactar observación |   |   | L | C |   |   |
| Guardar observación |   |   |   | A |   |   |
| Notificar al responsable | L |   |   | L | C |   |
| Actualizar estadísticas mensuales | L |   |   | L |   | A |

> **Leyenda:**  
> **C**: Crear – **L**: Leer/Listar – **A**: Actualizar – **E**: Eliminar  

---

## 2) Métodos identificados

> Los métodos se derivan directamente de las operaciones (C/L/A/E) marcadas en la tabla.  
> Cada método deberá existir en la clase correspondiente del **diagrama de clases**, y reflejarse en su **Tarjeta CRC** y en el **diagrama de secuencia** del caso de uso.

| Clase | Método | Tipo (C/L/A/E) | Parámetros (nombre: tipo) | Retorno | Actividad asociada |
|--------|---------|----------------|----------------------------|----------|--------------------|
| Proyecto | `listarProyectosActivos()` | L | — | `List<Proyecto>` | Seleccionar proyecto activo |
| Etapa | `listarEtapasPorProyecto(proyectoId: int)` | L | `proyectoId: int` | `List<Etapa>` | Elegir etapa correspondiente |
| Observación | `crearObservacion(etapaId: int, usuarioId: int, texto: string)` | C | `etapaId: int`, `usuarioId: int`, `texto: string` | `Observacion` | Redactar observación |
| Observación | `actualizarObservacion(id: int, texto: string)` | A | `id: int`, `texto: string` | `bool` | Guardar observación |
| Notificación | `enviarNotificacionResponsable(etapaId: int, mensaje: string)` | C | `etapaId: int`, `mensaje: string` | `bool` | Notificar al responsable |
| Reporte | `actualizarReporteMensual()` | A | — | `bool` | Actualizar estadísticas mensuales |

---

## 3) Relación con otros artefactos del diseño

| Elemento | Artefacto vinculado | Archivo / Referencia URL | Descripción de la relación |
|-----------|--------------------|---------------------------|-----------------------------|
| `listarProyectosActivos()` | Diagrama de Secuencia – CU4 | [`diagramas/05-diagramas-secuencia/04-secuencia-agregar-observacion.puml`]() | Se usa en el paso inicial para seleccionar un proyecto activo. |
| `crearObservacion()` | Tarjeta CRC – Observación | [`herramientas-agile/tarjetas-crc/crc-observacion.md`]() | Figura como responsabilidad principal de la clase. |
| `enviarNotificacionResponsable()` | Diagrama de Actividad – CU4 | [`diagramas/04-diagramas-actividades/04-actividad-agregar-observacion.puml`]() | Representa la acción final del flujo. |
| `actualizarReporteMensual()` | Diagrama de Secuencia – CU4 | [`diagramas/05-diagramas-secuencia/04-secuencia-agregar-observacion.puml`]() | Ejecutado al final del proceso, integrando los datos con el sistema de reportes. |
| `actualizarObservacion()` | Diagrama de Clases | [`diagramas/03-diagramas-clases/03-diagrama-clases-general.puml`]() | Define la operación A (Actualizar). |

---

## 4) Issues e inconsistencias detectadas

| URL | Descripción de la inconsistencia | Artefacto relacionado | Acción correctiva | Estado |
|------|----------------------------------|------------------------|-------------------|:------:|
| [#74](https://github.com/org/proyecto/issues/74) | `crearObservacion()` no figura en CRC de Observación | Tarjeta CRC – Observación | Agregar método y actualizar CRC | Resuelto |
| [#75](https://github.com/org/proyecto/issues/75) | Diagrama de secuencia CU4 no estaba vinculado al flujo de observaciones | Diagrama de Secuencia – CU4 | Integrado el diagrama actualizado (ver sección 3) | Resuelto |
| [#76](https://github.com/org/proyecto/issues/76) | `enviarNotificacionResponsable()` sin retorno declarado | Diagrama de Clases | Agregar tipo de retorno `bool` | Resuelto |
| [#77](https://github.com/org/proyecto/issues/77) | Falta vínculo con módulo de Reportes | Módulo de Reportes Estadísticos | Añadido método `actualizarReporteMensual()` | Pendiente |

**Estados posibles:** Abierto / Pendiente / Resuelto

---

## 5) Diagrama de Secuencia vinculado

```plantuml
@startuml 
title CU4 – Agregar Observaciones (flujo con actualización de estadísticas)

actor sistema
participant sistemaReportes as sistemaReportes
participant controlador as controlador
participant moduloEstadistico as moduloEstadistico
participant baseDeDatos as baseDeDatos

sistema -> sistemaReportes: detectaInicio (nuevoMes)
activate sistemaReportes
sistemaReportes -> controlador: solicitaDatos (mesAnterior) 
activate controlador
controlador -> moduloEstadistico: recopilaProyectos (entregados) 
activate moduloEstadistico
moduloEstadistico -> baseDeDatos: consultaProyectos (delMes)
activate baseDeDatos
baseDeDatos --> moduloEstadistico: datosDeProyectos
deactivate baseDeDatos
moduloEstadistico --> controlador: datosRecopilados 
deactivate moduloEstadistico
controlador --> sistemaReportes: datosProcesados
deactivate controlador
sistemaReportes --> sistema: tareaEjecutada
deactivate sistemaReportes

sistema -> sistemaReportes: activaGeneracionDeReporte
activate sistemaReportes
sistemaReportes -> controlador: procesaYGeneraReporte 
activate controlador
controlador -> moduloEstadistico: generaGraficos (yTablas) 
activate moduloEstadistico
moduloEstadistico -> baseDeDatos: obtieneDuracion (yTipos)
activate baseDeDatos 
baseDeDatos --> moduloEstadistico: informacionDeDuracion
deactivate baseDeDatos
moduloEstadistico --> controlador: graficosGenerados 
deactivate moduloEstadistico
controlador --> sistemaReportes: reportesEstadisticosListo
deactivate controlador 
sistemaReportes --> sistema: reporteDisponible
deactivate sistemaReportes

sistema -> sistemaReportes: programaElenvioAutomatico 
activate sistemaReportes
sistemaReportes -> controlador: enviaPorMail
activate controlador
controlador -> moduloEstadistico: preparaArchivos (pdf,Excel) 
activate moduloEstadistico
moduloEstadistico -> baseDeDatos: almacenaReporteGenerado 
activate baseDeDatos
baseDeDatos --> moduloEstadistico: confirmacionAlmacenamiento
deactivate baseDeDatos
moduloEstadistico --> controlador: archivoPreparado 
deactivate moduloEstadistico
controlador --> sistemaReportes: mailEnviadoAResponsable 
deactivate controlador
sistemaReportes --> sistema: notificacionEnviada 
deactivate sistemaReportes

destroy sistemaReportes
@enduml
