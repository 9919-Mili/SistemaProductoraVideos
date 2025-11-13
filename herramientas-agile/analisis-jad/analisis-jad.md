# Sesión JAD – Sistema de Gestión de Proyectos Audiovisuales

**Fecha:** 14/03/2025 – 11:00hs  
**Lugar:** Google Meet  
**Participantes:**  
- Laura González (Productora general – Vizion Estudio)  
- Martín Suárez (Responsable de Edición – Vizion Estudio)  
- Carla Paredes (Asistente de producción – Vizion Estudio)  
- Marcos Díaz (Analista funcional – SolucionesDev)  
- Julieta Romero (UX/UI – SolucionesDev)  

---

## 1) Objetivo de la sesión
Definir responsabilidades, reglas funcionales y restricciones del sistema orientado a objetos, para validar el modelo de clases y el flujo de trabajo representado en los **Casos de Uso 4 – Agregar Observaciones** y **5 – Consultar Estadísticas**.  
Se busca confirmar la interacción entre las clases `Observacion`, `Notificacion`, `Reporte` y `Estadistica`, además de las relaciones con `Proyecto`, `Etapa` y `Usuario`.

---

## 2) Matriz de Registro JAD
Mínimo 10 registros completos extraídos de la sesión.

| **Pregunta Clave (según guía JAD)** | **Respuesta / Decisión del Usuario** | **Clases Candidatas** | **Atributos / Métodos / Responsabilidades Detectadas** | **Observaciones** |
|------------------------------------|--------------------------------------|------------------------|--------------------------------------------------------|------------------|
| ¿Quién puede agregar una observación en un proyecto activo? | Solo usuarios con rol de *Responsable de Etapa* o *Productor General*. | `Usuario`, `Observacion` | `Usuario.rol`, `Observacion.crear()` | Validar permisos de escritura según tipo de usuario. |
| ¿Las observaciones deben quedar asociadas a una etapa o al proyecto completo? | A la etapa específica, no al proyecto general. | `Etapa`, `Observacion` | `Observacion.etapaId` | Se ajustará el modelo para mantener trazabilidad. |
| ¿Se requiere notificar a alguien cuando se crea una observación? | Sí, al responsable de la etapa correspondiente. | `Notificacion`, `Usuario` | `Notificacion.enviarNotificacionResponsable()` | Confirmar envío automático vía correo. |
| ¿Qué formato tendrán las observaciones? | Texto plano, sin adjuntos por ahora. | `Observacion` | `Observacion.texto`, `Observacion.fechaCreacion` | Podría evaluarse permitir archivos en una versión posterior. |
| ¿Cada observación puede editarse luego de guardada? | Solo por el usuario que la creó y mientras la etapa esté activa. | `Observacion`, `Etapa`, `Usuario` | `Observacion.actualizarObservacion()` | Añadir restricción lógica de edición. |
| ¿El sistema debe generar estadísticas de observaciones o entregas? | Principalmente de entregas y duración de proyectos. | `Estadistica`, `Proyecto` | `Estadistica.generarEstadisticas()`, `Proyecto.obtenerDuracionProyecto()` | Se incluirá análisis de cumplimiento por etapa. |
| ¿Qué tipo de filtros debe tener el módulo de estadísticas? | Por tipo de proyecto, fecha de inicio y fecha de fin. | `FiltroBusqueda` | `FiltroBusqueda.crearFiltro()` | Confirmado para el CU5. |
| ¿Quién puede acceder al módulo de estadísticas? | Solo usuarios autenticados con rol *Productor General*. | `Usuario` | `Usuario.autenticarUsuario()` | Se limita la vista a nivel de acceso administrativo. |
| ¿Los reportes deben descargarse o solo visualizarse? | Ambos: el usuario puede generar y descargar el reporte. | `Reporte`, `Estadistica` | `Reporte.generarReporte()` | El formato será PDF y Excel. |
| ¿Se almacenan los reportes generados? | Sí, para mantener histórico de consultas. | `Reporte`, `BaseDeDatos` | `Reporte.fechaGeneracion`, `Reporte.pathArchivo` | El controlador los guarda en la base de datos. |

---

## 3) Issues e inconsistencias detectadas

| **ID** | **Descripción del Issue / Inconsistencia** | **Impacto** | **Estado** | **Link a Issue (GitHub)** |
|--------|---------------------------------------------|--------------|-------------|-----------------------------------|
| #84 | No estaba definida la clase `Notificacion` en el modelo inicial. | Alto | Resuelto | [🔗 Issue #84 – Add Notificacion class](https://github.com/tu-org/SistemaProductoraVideos/issues/84) |
| #85 | Faltaba método `actualizarObservacion()` en clase Observación. | Medio | Resuelto | [🔗 Issue #85 – Update Observacion class methods](https://github.com/tu-org/SistemaProductoraVideos/issues/85) |
| #86 | Los filtros de estadísticas no contemplaban rango de fechas. | Medio | Pendiente | [🔗 Issue #86 – Extend FiltroBusqueda entity](https://github.com/tu-org/SistemaProductoraVideos/issues/86) |
| #87 | No se consideró la persistencia de reportes generados. | Alto | Pendiente | [🔗 Issue #87 – Store generated reports](https://github.com/tu-org/SistemaProductoraVideos/issues/87) |
| #88 | Reglas de edición de observaciones no reflejadas en el modelo. | Medio | Pendiente | [🔗 Issue #88 – Restrict Observacion edition](https://github.com/tu-org/SistemaProductoraVideos/issues/88) |

---

## 4) Conclusiones
La sesión permitió validar la relación entre los módulos **de seguimiento (Observaciones)** y **de análisis (Estadísticas)**, definiendo reglas claras para su integración en el sistema orientado a objetos.  
Se acordó mantener el principio de trazabilidad por *Etapa*, reforzar los permisos por *Rol de Usuario* y garantizar la generación automatizada de **reportes estadísticos mensuales**.  
Los hallazgos de esta sesión se derivarán al **Especialista en Diagramas de Clases** para actualizar las relaciones y dependencias identificadas.

---
