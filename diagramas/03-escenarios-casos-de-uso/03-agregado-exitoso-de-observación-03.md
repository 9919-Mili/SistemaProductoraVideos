| **Nombre del escenario:** | Agregado exitoso de observación | | | |
|---|---|---|---|---|
| **Nombre del caso de uso:** | Agregar Observaciones | | **ID Única:** | 3 |
| **Área** | Sistema Productora de Videos, Gestión de comentarios | | | |
| **Actor(es):** | Productora General, Responsable de la Etapa, Asistente de Producción | | | |
| **Descripción:** | Los usuarios autorizados agregan comentarios generales o internos en las etapas de los proyectos, facilitando la comunicación y el seguimiento. | | | |

| **Activar Evento:** | El actor selecciona la etapa del proyecto, escribe la observación y la confirma.. | **Identificadores e iniciadores de caso de uso** |
|---|---|---|
| **Tipo de señal:** | ☑️ Externa | ☐ Temporal | |

| **Pasos desempeñados (ruta principal)** | **Información para los pasos** |
|---|---|
| 1. El actor accede al sistema | Usuario autenticado con permisos sobre la etapa |
| 2. El sistema presenta su panel principal | Panel principal el sistema |
| 3. El actor selecciona el proyecto correspondiente | Listado de proyectos activos en el panel principal del sistema |
| 4. El sistema presenta el panel del proyecto seleccionado | Panel de características y etapas del proyecto |
| 5. El actor elige la etapa donde agregar observación | Listado de etapas asociadas al proyecto |
| 6. El sistema presenta el panel de la etapa seleccionada | Panel de características y etapas del proyecto |
| 7. El actor escribe el comentario en el campo de observaciones | Formulario web de observaciones en el panel |
| 8. El actor añade detalles adicionales si corresponde | Campos opcionales para adjuntos o etiquetas del panel|
| 10. El actor confirma y guarda el comentario | Botón de confirmación en la interfaz |
| 11. El sistema registra la observación y envía notificación | Registro en base de datos, envío de mail y WhatsApp |
| 12. La observación queda visible en el historial de la etapa | Visualización inmediata para los involucrados |

| **Condiciones, suposiciones y preguntas** | |
|---|---|
| **Precondiciones:** | El usuario está autenticado y tiene permisos para comentar. |
| **Poscondiciones:** | La observación queda asociada al proyecto/etapa y notificada a los involucrados. |
| **Suposiciones:** | El usuario tiene acceso al sistema y los datos necesarios. Existe un proyecto y etapa en el sitema. El sistema está operativo y conectado a la base de datos. |
| **Reunir requerimentos:** | Requisito Funcional 1 (Visualización de proyectos y etapas)-2 (Notificaciones automáticas)-3 (Agregado de adjuntos)-5 (Gestión de etapas) |
| **Aspectos sobresalientes:** | ¿se pueden editar o eliminar observaciones? ¿quién recibe las notificaciones? ¿se pueden adjuntar archivos? |
| **Prioridad:** | Baja |

| **Riesgo:** | Bajo |
