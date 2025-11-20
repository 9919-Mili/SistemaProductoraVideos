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
La sesión tuvo como objetivo definir los aspectos funcionales y estructurales del Sistema de Gestión de Proyectos Audiovisuales. A partir de estos requisitos, se pueden definir numerosos casos de uso centrados en la gestión, configuración, seguimiento y notificación.

---

## 2) Matriz de Registro JAD
Mínimo 10 registros completos extraídos de la sesión.

| **Pregunta Clave** | **Decisión del Usuario** | **Clases Candidatas** | **Atributos / Métodos / Responsabilidades Detectadas** | **Observaciones** |
|------------------------------------|--------------------------------------|------------------------|--------------------------------------------------------|------------------|
| ¿Quién puede agregar una observación en un proyecto activo? | Solo usuarios con rol de *Responsable de Etapa* o *Productor General*. | `Usuario`, `Observacion` | `Usuario.rol`, `Observacion.crear()` | Validar permisos de escritura según tipo de usuario. |
| ¿Las observaciones deben quedar asociadas a una etapa o al proyecto completo? | A la etapa específica, no al proyecto general. | `Etapa`, `Observacion` | `Observacion.etapaId` | Se ajustará el modelo para mantener trazabilidad. |
| ¿Se requiere notificar a alguien cuando se crea una observación? | Sí, al responsable de la etapa correspondiente. | `Notificacion`, `Usuario` | `Notificacion.enviarNotificacionResponsable()` | Confirmar envío automático vía correo. |
| ¿Qué formato tendrán las observaciones? | Texto plano, sin adjuntos por ahora. | `Observacion` | `Observacion.texto`, `Observacion.fechaCreacion` | Podría evaluarse permitir archivos en una versión posterior. |
| ¿Cada observación puede editarse luego de guardada? | Solo por el usuario que la creó y mientras la etapa esté activa. | `Observacion`, `Etapa`, `Usuario` | `Observacion.actualizarObservacion()` | Añadir restricción lógica de edición. |
| ¿El sistema debe generar estadísticas de observaciones o entregas? | Principalmente de entregas y duración de proyectos. | `Estadistica`, `Proyecto` | `Estadistica.generarEstadisticas()`, `Proyecto.obtenerDuracionProyecto()` | Se incluirá análisis de cumplimiento por etapa. |
| ¿Qué tipo de filtros debe tener el módulo de estadísticas? | Por estado, responsable y tipo de proyecto. | `FiltroBusqueda` | `FiltroBusqueda.crearFiltro()` | Confirmado para el CU5. |
| ¿Quién puede acceder al módulo de estadísticas? | Solo usuarios autenticados con rol *Productor General*. | `Usuario` | `Usuario.autenticarUsuario()` | Se limita la vista a nivel de acceso administrativo. |
| ¿Los reportes deben descargarse o solo visualizarse? | Ambos: el usuario puede generar y descargar el reporte. | `Reporte`, `Estadistica` | `Reporte.generarReporte()` | El formato será PDF y Excel. |
| ¿Se almacenan los reportes generados? | Sí, para mantener histórico de consultas. | `Reporte`, `BaseDeDatos` | `Reporte.fechaGeneracion`, `Reporte.pathArchivo` | El controlador los guarda en la base de datos. |

---

## 3) Issues e inconsistencias detectadas

| **ID** | **Descripción del Issue / Inconsistencia** | **Impacto** | **Estado** | **Link a Issue (GitHub)** |
|--------|---------------------------------------------|--------------|-------------|-----------------------------------|
| #82 |Falta tarjeta CRC “Crear Etapa” en clase Etapa. Falta acción “notificarCambio” en el diagrama de secuencias. Método CrearEtapas() sin tipo de retorno.| Alto | Resuelto | 🔗 https://github.com/9919-Mili/SistemaProductoraVideos/issues/82|
| #83 | Acción “AsignarResponsable” no aparece en el diagrama de secuencia. Método asignarResponsables() sin tipo de retorno.| Medio | Resuelto | 🔗 https://github.com/9919-Mili/SistemaProductoraVideos/issues/83 |
| #84 | Falta tarjeta CRC “buscarCliente” en Proyecto. Falta acción “buscarCliente” en el diagrama de secuencia.| Alto | Resuelto | 🔗 https://github.com/9919-Mili/SistemaProductoraVideos/issues/84|
| #85 | Falta tarjeta CRC de Notificación (05-tarjeta-crc-notificacion.md). | Bajo | Resuelto | 🔗 https://github.com/9919-Mili/SistemaProductoraVideos/issues/85|
| #89 | Falta acción “seleccionarUsuario” en el diagrama de secuencias. | Bajo | Resuelto | 🔗 https://github.com/9919-Mili/SistemaProductoraVideos/issues/89 |

---

## 4) Conclusiones
La sesión permitió validar la relación entre los módulos **de seguimiento (Observaciones)** y **de análisis (Estadísticas)**, definiendo reglas claras para su integración en el sistema orientado a objetos.  
Se acordó mantener el principio de trazabilidad por *Etapa*, reforzar los permisos por *Rol de Usuario* y garantizar la generación automatizada de **reportes estadísticos mensuales**.  
Los hallazgos de esta sesión se derivarán al **Especialista en Diagramas de Clases** para actualizar las relaciones y dependencias identificadas.

---
