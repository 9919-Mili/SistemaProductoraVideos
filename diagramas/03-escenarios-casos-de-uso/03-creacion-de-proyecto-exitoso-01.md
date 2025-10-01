| **Nombre del escenario:** | Creación de Proyecto exitoso | | | |
|---|---|---|---|---|
| **Nombre del caso de uso:** | Creación de Proyecto | | **ID Única:** | 1 |
| **Área** | Sistema Productora de Videos, Gestión de proyectos | | | |
| **Actor(es):** | Productora General | | | |
| **Descripción:** | Permite a la Productora General registrar un nuevo proyecto, ingresando nombre, tipo, fechas y responsables, para su seguimiento y gestión en el sistema. | | | |

| **Activar Evento:** | El actor selecciona la opción “Crear Proyecto” | **Identificadores e iniciadores de caso de uso** |
|---|---|---|
| **Tipo de señal:** | ☑️ Externa | ☐ Temporal | |

| **Pasos desempeñados (ruta principal)** | **Información para los pasos** |
|---|---|
| 1. El actor ingresa al sistema | Usuario autenticado con permisos de Productora General |
| 2. El actor oprime el botón “Crear Proyecto” | Botón visible en el panel principal del sistema |
| 3. El sistema proporciona un formulario de registro para cargar los datos | Formulario web de registro de proyecto |
| 4.  El actor completa los campos obligatorios (nombre, tipo, fechas, responsables) del formulario | Formulario web de registro de proyecto |
| 5. El actor oprime el botón "Confirma la creación del proyecto" | Formulario web de registro de proyecto |
| 6. El sistema valida los datos y guarda la información | Validación de campos y registro en la base de datos |
| 7. El sistema muestra el nuevo proyecto en el tablero de control | Visualización inmediata en la interfaz principal |
| 8. Se notifican automáticamente los responsables asignados | Notificación por correo y WhatsApp |

| **Condiciones, suposiciones y preguntas** | |
|---|---|
| **Precondiciones:** | El usuario del actor está autenticado como Productora General. |
| **Poscondiciones:** | El proyecto queda registrado y disponible para seguimiento. |
| **Suposiciones:** | El actor tiene todos los datos necesarios para el formulario. El sistema está operativo y conectado a la base de datos. |
| **Reunir requerimentos:** | Requisito Funcional 1(Visualización de proyectos)-2(Notificaciones automáticas) |
| **Aspectos sobresalientes:** | ¿hay requisitos en la información a ingresar en los campos del formulario? ¿qué ocurre si falta algún dato obligatorio? ¿hay otro proyecto identico al actual en el sistemas ahora?|
| **Prioridad:** | Alta |
| **Riesgo:** | Alto |
