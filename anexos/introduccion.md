# Anexo - Introducción al Diseño Orientado a Objetos

## Descripción del paradigma orientado a objetos:
El paradigma orientado a objetos se trata de un enfoque para el diseño de programas que se concentra en como el usuario percibe las cosas o eventos en un sistema alrededor de los objetos. Su importancia radica en que permite a los usuarios el visualizar el comportamiento de un programa en "objetos" sencillamente identificables con sus relativos del mundo real, en lugar del enfoque clasico de tareas.

## Los cuatro fundamentos de POO:

<<<<<<< HEAD
### Abstracción

### Herencia

### Polimorfismo

### Encapsulación

=======
### Abstracción
La abstracción consiste en identificar y modelar las características esenciales de un objeto, ignorando los detalles irrelevantes para representar entidades del mundo real mediante clases u objetos, enfocándose solo en los atributos y comportamientos necesarios para facilitar la comprensión, reutilización y mantenimiento por parte del usuario.

### Herencia
La herencia es un mecanismo que permite crear nuevas clases que hereden los atributos y métodos de clases existentes, lo que facilita la reutilización de código y la organización jerárquica de las clases.

### Polimorfismo
El polimorfismo es la capacidad de los objetos de diferentes clases relacionadas por herencia de responder a la misma operación o método de distintas formas. Esto permite que diferentes tipos de objetos, compartan clases de manera flexible sin atarse ciertos atributos o comportamientos que estan definidos en un clase.

### Encapsulación
La encapsulación es el principio que consiste en ocultar las características de una clase u objeto, y exponer solo lo necesario a procesos externos que interactuen con sus datos. Esto protege los datos y el funcionamiento interno del objeto, permitiendo que solo se acceda o modifique mediante métodos específicos.


>>>>>>> 5373de06309dab124f0ce75050992b6772335e43
## Requisistos iniciales del sistema

<<<<<<< HEAD
### Requisitos funcionales
=======
### Requisitos funcionales
1 - El sistema permitira crear nuevas etapas de los proyectos, de ser necesario.  
2 - Notificara por mail o wpp cualquier tipo de modificacion, retraso, pendientes, o si esta listo el proyecto.  
3 - Generara estadisticas mensuales de demoras o cantidad de proyectos, las filtrara por cliente.  
4 - Tendra que tener un tablero de uso interno, en el que se pueda visualizar los proyectos de cada cliente, cantidad, y por quien estan elaborados.
>>>>>>> 5373de06309dab124f0ce75050992b6772335e43

<<<<<<< HEAD
=======
### Requisitos no funcionales
1 - El sistema debe funcionar de forma correcta, y notificar a la brevedad cualquiero cambio.   
2 - El sistema debe poder abrirse en cuaquier tipo de dispositivo.  
3 - Al sistema solo tendran acceso las personas encargadas de trabajar en los proyectos.   
4 - El sistema debera funcionar las 24hs. 
>>>>>>> 5373de06309dab124f0ce75050992b6772335e43

### Requisitos no funcionales


## Casos de uso:
<<<<<<< HEAD


=======

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
>>>>>>> 5373de06309dab124f0ce75050992b6772335e43