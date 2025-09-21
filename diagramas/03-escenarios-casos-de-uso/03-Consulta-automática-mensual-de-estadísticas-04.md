| **Nombre del escenario:** | Consulta automática mensual de estadísticas | | | |
|---|---|---|---|---|
| **Nombre del caso de uso:** | Consultar Estadísticas | | **ID Única:** | 4 |
| **Área** | Sistema Productora de Videos, Módulo de reportes y estadísticas | | | |
| **Actor(es):** | Productora General, Responsable de la Etapa | | | |
| **Descripción:** | El sistema genera y envía automáticamente un reporte mensual de estadísticas sobre proyectos entregados, duración y tipo, sin intervención directa del usuario. | | | |

| **Activar Evento:** | El sistema ejecuta una tarea programada el primer día de cada mes, genera el reporte de estadísticas. | **Identificadores e iniciadores de caso de uso** |
|---|---|---|
| **Tipo de señal:** | ☐ Externa | ☑️ Temporal | |

| **Pasos desempeñados (ruta principal)** | **Información para los pasos** |
|---|---|
| 1. El sistema detecta el inicio de un nuevo mes | Tarea programada en el servidor |
| 2. Recopila los datos de proyectos entregados, duración y tipo del mes anterior | Acceso a la base de datos de proyectos |
| 3. Procesa y genera el reporte estadístico | Generación automática de gráficos y tablas |
| 4. Envía el reporte por correo electrónico a los responsables | Envío automático a los usuarios registrados de los actores|
| 5. Los actores reciben el reporte en su bandeja de entrada | Archivo adjunto en formato PDF o Excel |
| 6. El reporte queda disponible en el módulo de estadísticas para consulta posterior | Almacenamiento en el sistema para acceso histórico |

| **Condiciones, suposiciones y preguntas** | |
|---|---|
| **Precondiciones:** | Deben existir proyectos registrados y usuarios responsables configurados para recibir reportes. |
| **Poscondiciones:** | Los usuarios reciben el reporte mensual y pueden consultarlo en cualquier momento. |
| **Suposiciones:** | El sistema está operativo y la tarea programada funciona correctamente. Los correos de los usuarios están actualizados. |
| **Reunir requerimentos:** | Requisito Funcional 2 (Notificaciones automáticas)-3 (Adjuntar y almacenar enlaces externos)-4 (Generación de reportes mensuales) |
| **Aspectos sobresalientes:** | ¿se puede modificar la periodicidad? ¿qué ocurre si falla el envío? ¿el reporte se almacena para consulta histórica? |
| **Prioridad:** | Alta |
| **Riesgo:** | Medio |