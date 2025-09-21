**Nombre del escenario:** |  Consulta exitosa de proyectos activos | | | |
|---|---|---|---|---|
| **Nombre del caso de uso:** | Consultar Proyectos Activos | | **ID Única:** | 5 |
| **Área** | Sistema Productora de Videos, Gestión de Proyectos | | | |
| **Actor(es):** | Productora General, Responsable de la Etapa, Asistente de Producción | | | |
| **Descripción:** | Permite a los actores ver el estado actual de los proyectos en curso, filtrar por responsable o etapa, consultar detalles y añadir observaciones para verificar el avance y cumplimiento. | | | |

| **Activar Evento:** | El actor selecciona “Proyectos Activos” y filtra un proyecto en curso. | **Identificadores e iniciadores de caso de uso** |
|---|---|---|
| **Tipo de señal:** | ☑️ Externa | ☐ Temporal | |

| **Pasos desempeñados (ruta principal)** | **Información para los pasos** |
|---|---|
| 1. El actor accede al sistema | Usuario autenticado con permisos para consultar proyectos |
| 2. El sistema presenta su panel principal | Panel principal el sistema |
| 3. El actor selecciona la opción “Proyectos Activos” | Opción disponible en el menú principal |
| 3. El sistema lista los proyectos en curso | Visualización en el panel de control |
| 4. El actor filtra por responsable o etapa | Filtros disponibles en la interfaz |
| 5. El actor selecciona un proyecto para ver más detalles | Acceso al panel del proyecto |
| 6. El sistema muestra estado, responsables y cumplimiento | Información detallada y actualizada |
| 7. El actor puede añadir observaciones desde este módulo | Formulario de observaciones integrado |
| 8. El sistema registra la observación y la asocia al proyecto/etapa | Registro en base de datos y notificación automática |

| **Condiciones, suposiciones y preguntas** | |
|---|---|
| **Precondiciones:** | El usuario está autenticado y existen proyectos en curso. |
| **Poscondiciones:** | El usuario obtiene la lista de proyectos activos con información actualizada y puede añadir observaciones. |
| **Suposiciones:** | El sistema tiene proyectos en curso y el usuario conoce los filtros que desea aplicar. |
| **Reunir requerimentos:** | Requisito Funcional 1 (Visualización de proyectos y etapas)-2 (Notificaciones automáticas)-3 (Agregado de adjuntos)|
| **Aspectos sobresalientes:** | ¿se pueden exportar los datos? ¿se pueden ver los cambios históricos de estado? |
| **Prioridad:** | Alta |
| **Riesgo:** | Bajo |