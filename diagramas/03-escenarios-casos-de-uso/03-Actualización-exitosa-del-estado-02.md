| **Nombre del escenario:** | Actualización exitosa del estado de la etapa | | | |
|---|---|---|---|---|
| **Nombre del caso de uso:** | Actualizar Estado de la Etapa | | **ID Única:** | 2 |
| **Área** | Sistema Productora de Videos, Gestión de etapas de proyecto | | | |
| **Actor(es):** | Responsable de la Etapa | | | |
| **Descripción:** | Permite al responsable de una etapa modificar y notificar el estado de la misma (pendiente, en curso, pausado, finalizado) para mantener actualizado el avance del proyecto. | | | |

| **Activar Evento:** | El actor selecciona el proyecto y la etapa, indica el nuevo estado y confirma la actualización.. | **Identificadores e iniciadores de caso de uso** |
|---|---|---|
| **Tipo de señal:** | ☑️ Externa | ☐ Temporal | |

| **Pasos desempeñados (ruta principal)** | **Información para los pasos** |
|---|---|
| 1. El actor accede al sistema | Usuario autenticado con permisos sobre la etapa |
| 2. El sistema presenta su panel principal | Panel principal el sistema |
| 3. El actor selecciona el proyecto correspondiente | Listado de proyectos activos en el panel principal del sistema |
| 4. El sistema presenta el panel del proyecto seleccionado | Panel de características y etapas del proyecto |
| 5. El actor elige la etapa que desea actualizar | Listado de etapas asociadas al proyecto |
| 6. El sistema presenta el panel de la etapa seleccionada | Panel de características y etapas del proyecto |
| 7. El actor indica el nuevo estado de la etapa | Menú desplegable con opciones de estado |
| 8. El actor confirma el cambio de estado | Botón de confirmación en la interfaz |
| 9. El sistema guarda la actualización y envía notificaciones | Registro en base de datos, envío de mail y WhatsApp |
| 10. El nuevo estado queda visible en el tablero de control | Visualización inmediata para todos los involucrados |

| **Condiciones, suposiciones y preguntas** | |
|---|---|
| **Precondiciones:** | La etapa existe y está asociada a un proyecto activo. El usuario del actor está autenticado como Responsable de la Etapa a actualizar. |
| **Poscondiciones:** | El estado de la etapa queda actualizado y visible para los involucrados. |
| **Suposiciones:** | El sistema está operativo y conectado a la base de datos. |
| **Reunir requerimentos:** | Requisito Funcional 1 (Visualización de proyectos y etapas)-2 (Notificaciones automáticas)-5 (Gestión de etapas) |
| **Aspectos sobresalientes:** | ¿se puede bloquear el cambio a algun estado especifico? ¿puede estar bloqueada la lista desplegable de estados? ¿se puede cambiar al mismo etado en que la etapa esta actualmente? |
| **Prioridad:** | Media |
| **Riesgo:** | Alto |