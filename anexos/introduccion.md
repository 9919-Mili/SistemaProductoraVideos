# Anexo - Introducción al Diseño Orientado a Objetos

## Descripción del paradigma orientado a objetos:
El paradigma orientado a objetos se trata de un enfoque para el diseño de programas que se concentra en como el usuario percibe las cosas o eventos en un sistema alrededor de los objetos. Su importancia radica en que permite a los usuarios el visualizar el comportamiento de un programa en "objetos" sencillamente identificables con sus relativos del mundo real, en lugar del enfoque clasico de tareas.

## Los cuatro fundamentos de POO:

### Abstracción
La abstracción consiste en identificar y modelar las características esenciales de un objeto, ignorando los detalles irrelevantes para representar entidades del mundo real mediante clases u objetos, enfocándose solo en los atributos y comportamientos necesarios para facilitar la comprensión, reutilización y mantenimiento por parte del usuario.

### Herencia
La herencia es un mecanismo que permite crear nuevas clases que hereden los atributos y métodos de clases existentes, lo que facilita la reutilización de código y la organización jerárquica de las clases.

### Polimorfismo
El polimorfismo es la capacidad de los objetos de diferentes clases relacionadas por herencia de responder a la misma operación o método de distintas formas. Esto permite que diferentes tipos de objetos, compartan clases de manera flexible sin atarse ciertos atributos o comportamientos que estan definidos en un clase.

### Encapsulación
La encapsulación es el principio que consiste en ocultar las características de una clase u objeto, y exponer solo lo necesario a procesos externos que interactuen con sus datos. Esto protege los datos y el funcionamiento interno del objeto, permitiendo que solo se acceda o modifique mediante métodos específicos.

### Ejemplos

- La abstracción: se abstrajeron los archivos audio, imagen y pdf que dieron los clientes para extraer lo mas esencial tanto de los requisitos del proyecto, las clases de uso y principalmente en el diagrama "01-boceto-inicial" de clases, con cada una que se les definieron atributos y métodos.   
- El polimorfismo: se podría aplicar a subclases de la clase Estadistica, entre estas pueden variar para clasificar subclases que correspondan a distintos tipos de datos como "tipo: int" para una estadistica númerica de cantidad de proyectos o "tipo: String" para los tipos de cliente.   
- La herencia: se puede usar la clase Adjunto como ejemplo, esta puede contener subclases referentes a archivos de cada pagina como Vimeo o Drive, estas clases heredarian atributos como "url" y el método de "vincularRecurso()".
- Encapsulación: la clase Etapa que esta directamente relacionada con las clases Usuario, Adjunto y Comentario no es modificada directamente cuando se utiliza cualquier método de esas otras clases, como "agregarComentario()", sino que esta encapsulada para que solo sea modificada una vez se utiliza el método "actualizarEstado()".

## Requisistos iniciales del sistema

### Requisitos funcionales
1. El sistema debe mostrar el estado actual de al menos 20 proyectos activos simultáneamente en un panel de control general o tablero, actualizando la información en un máximo de 5 segundos tras cualquier cambio de estado. Esto permitirá ver "en qué estado está cada uno de un vistazo" y "el estado de todos los proyectos y etapas".
2.  El sistema debe enviar notificaciones automáticas por correo electrónico y WhatsApp en menos de 60 segundos cuando una etapa se completa o cuando se asigna una nueva tarea o responsable. Esto responde a la necesidad de "avisar automáticamente por mail o WhatsApp cuando se completa una etapa o cuando se asigna una nueva tarea" y que "el sistema avise automáticamente a quien sigue".   
3. El sistema debe permitir adjuntar y almacenar hasta 10 enlaces externos (como a carpetas de Drive o videos de Vimeo/Bimio) por cada etapa de un proyecto, garantizando su persistencia y acceso rápido en todo momento. La intención es "poder registrar esos enlaces dentro del sistema para tener todo en un solo lugar" y "subir links a Drive, Vimeo u otras plataformas para no perderlos   
4. El sistema debe generar reportes mensuales de al menos 3 tipos de estadísticas (ej., proyectos entregados, tiempo promedio por etapa, proyectos por tipo), con la capacidad de filtrar estos datos por cliente y por tipo de proyecto (publicidad, videoclip, institucional), y con un tiempo de respuesta de la consulta no superior a 10 segundos
5. El sistema debe permitir a un usuario con permisos de administrador definir y añadir hasta 5 nuevas etapas personalizadas por proyecto en un tiempo máximo de 30 segundos, adaptándose a las necesidades específicas y variantes de cada tipo de proyecto. Para poder crear nuevas etapas si hace falta y la flexibilidad para agregar o quitar etapas según el tipo de proyecto.   

### Requisitos no funcionales
1. El sistema debe ser completamente accesible y funcional vía web desde cualquier navegador moderno en dispositivos de escritorio y móviles, asegurando que el 99% de sus funcionalidades estén disponibles y sean usables en ambas plataformas
2. Un nuevo usuario, sin entrenamiento formal previo, debe ser capaz de realizar las acciones básicas de carga y actualización de un proyecto (nombre, etapas, responsable, estado) en menos de 5 minutos, utilizando una interfaz simple e intuitiva. 
3. Las principales vistas del sistema, como el "tablero de control" o el "panel general" de proyectos, deben cargar completamente en menos de 3 segundos bajo una carga de 20 proyectos activos y 10 usuarios concurrentes. Esto es fundamental para que el equipo pueda ver en qué estado está cada uno de un vistazo y para evitar la pérdida de tiempo. 
4.  El sistema debe garantizar que el 100% de la información ingresada (proyectos, etapas, enlaces, comentarios, etc.) se mantenga persistente y sea recuperable en todo momento tras cualquier recarga de la página o reinicio del sistema
5. El sistema debe ser capaz de soportar la gestión simultánea de al menos 50 proyectos activos y 20 usuarios concurrentes sin que el tiempo de respuesta de las acciones clave exceda los 5 segundos.

## Casos de uso:

### Creación de Proyecto
**Actor(es):** Productora General / Laura González  
**Descripción breve:** Incorporar proyectos nuevos agregando todos los campos (nombre, tipo, fechas, responsables).  
**Flujo principal de eventos:**
1. La Productora General ingresa al sistema.  
2. Oprime el botón rápido “Crear Proyecto”.  
3. Completa los campos obligatorios.  
4. Revisa la información ingresada.  
5. Confirma la creación del proyecto.  
6. El sistema valida los datos y guarda la información.  
**Precondiciones:** El usuario debe estar autenticado como Productora General.  
**Postcondiciones:** El proyecto queda registrado en el sistema y disponible para seguimiento.  

---

### Actualizar Estado de la Etapa
**Actor(es):** Responsable de la Etapa  
**Descripción breve:** Notificar el estado de la etapa: pendiente, en curso, pausado, finalizado.  
**Flujo principal de eventos:**
1. El Responsable de la Etapa accede al sistema.  
2. Selecciona el proyecto correspondiente.  
3. Elige la etapa que desea actualizar.  
4. Indica el nuevo estado.  
5. Revisa la información.  
6. Confirma el cambio de estado.  
7. El sistema guarda la actualización y envía notificaciones por mail o WhatsApp.  
**Precondiciones:** La etapa debe existir y estar asociada a un proyecto activo.  
**Postcondiciones:** El estado queda actualizado y visible a los involucrados.  

---

### Agregar Observaciones
**Actor(es):** Productora General / Laura González, Responsable de la Etapa, Asistente de Producción / Carla Paredes  
**Descripción breve:** Agregar comentarios generales o internos.  
**Flujo principal de eventos:**
1. El usuario accede al sistema.  
2. Selecciona el proyecto y la etapa correspondiente.  
3. Escribe el comentario en el campo de observaciones.  
4. Añade detalles adicionales si corresponde.  
5. Revisa la observación.  
6. Confirma y guarda el comentario.  
7. El sistema registra la observación y envía notificación.  
**Precondiciones:** El usuario debe estar autenticado.  
**Postcondiciones:** La observación queda asociada al proyecto/etapa.  

---

### Consultar Estadísticas
**Actor(es):** Productora General / Laura González, Responsable de la Etapa  
**Descripción breve:** Consultar estadísticas sobre proyectos entregados por mes, duración y tipo.  
**Flujo principal de eventos:**
1. El usuario accede al sistema.  
2. Selecciona el módulo “Estadísticas”.  
3. Define filtros (tipo, rango de fechas, etc.).  
4. Solicita la consulta.  
5. El sistema procesa y genera reportes.  
6. El usuario visualiza o descarga los resultados.  
**Precondiciones:** Deben existir proyectos registrados.  
**Postcondiciones:** El usuario obtiene estadísticas actualizadas.  

---

### Consultar Proyectos Activos
**Actor(es):** Productora General / Laura González, Responsable de la Etapa, Asistente de Producción / Carla Paredes  
**Descripción breve:** Ver el estado actual del proyecto para verificar su avance y cumplimiento.  
**Flujo principal de eventos:**
1. El usuario accede al sistema.  
2. Selecciona la opción “Proyectos Activos”.  
3. El sistema lista los proyectos en curso.  
4. El usuario filtra por responsable o etapa.  
5. Selecciona un proyecto para más detalles.  
6. El sistema muestra estado, responsables y cumplimiento.  
7. El usuario puede añadir observaciones desde este módulo.  
**Precondiciones:** El usuario debe estar autenticado y existir proyectos en curso.  
**Postcondiciones:** El usuario obtiene la lista de proyectos activos con información actualizada.

### Boceto inicial del diseño de clases
---
[Diagrama 01 - Boceto Inicial](/diagramas/01-diagrama-clases/01-boceto-inicial.png)   

![diagrama-boceto-01](/diagramas/01-diagrama-clases/01-boceto-inicial.png)
