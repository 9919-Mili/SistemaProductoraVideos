# Patrones de Diseño de Comportamiento – Observer

## Propósito y Tipo del Patrón

El proposito del Patrón es permitir que cambios en el estado de elementos críticos del dominio —**Proyecto**, **Etapa** y **Tarea**— generen notificaciones automáticas a las distintas áreas del sistema sin acoplar estas entidades a los módulos de notificación, auditoría o visualización.

**Patrón de Comportamiento — Observer.**  
Define una relación de suscripción entre objetos: cuando un Subject cambia su estado, informa automáticamente a todos los Observers registrados.

## Cómo se relaciona con SOLID

Los patrones de diseño de comportamiento definen **cómo los objetos interactúan entre sí** y cómo distribuyen responsabilidades sin generar rigidez.  
Este tipo de patrón permite que los cambios en un objeto se propaguen a otros sin que exista una dependencia directa entre ellos.

### SOLID

- **S – Responsabilidad Única:** cada clase gestiona un único motivo de cambio, ejemplo: el Subject gestiona su estado; los Observers gestionan sus reacciones.  
- **O – Abierto/Cerrado:** pueden agregarse nuevos observadores sin modificar las clases ya existentes.  
- **L – Sustitución de Liskov:** cualquier observador puede sustituirse si implementa la misma interfaz.  
- **I – Segregación de Interfaces:** los observadores implementan solo la interfaz Observer con el método estrictamente necesario.  
- **D – Inversión de Dependencias:** tanto Subject como Observer dependen de una abstracción, no de una implementación concreta.
---

## Motivación

Durante la sesión JAD, las matrices CLAE y el análisis del diagrama final de clases, se observó un problema transversal:
Varias clases debían reaccionar cuando una **Etapa** o **Tarea** cambiaba su estado:  
- Servicio de Notificaciones  
- Responsable del Proyecto  
- Coordinador  
- Servicio de Auditoría  
- Dashboard del Administrador  
- Cliente  
- Módulos de calendarización y métricas  

Sin el patrón Observer, estas reacciones estaban:

- Distribuidas dentro de Proyecto, Etapa y Tarea  
- Mezcladas con lógica propia del dominio  
- Duplicadas en distintos métodos  
- Dependiendo de servicios concretos (violando DIP)  
- Impidiendo agregar nuevos interesados sin modificar varias clases  
- Provocando un acoplamiento rígido hacia la infraestructura  

### Cómo lo soluciona el patrón

El patrón Observer permite:

- Que **Proyecto**, **Etapa** y **Tarea** actúen como *Subject*  
- Que las clases interesadas (Notificaciones, Auditoría, Responsable, Dashboard, etc.) actúen como *Observers*  
- Que la notificación de cambios sea automática y desacoplada  
- Agregar observadores sin modificar las clases del dominio  
- Asegurar que la lógica de negocio permanezca limpia y centrada en su responsabilidad  
- Cumplir con principios SOLID y con las necesidades de escalabilidad del sistema  

### Clases implicadas
El patrón Observer se aplica sobre un conjunto de clases del dominio que, según el análisis JAD y las mejoras CRC, presentan cambios de estado que afectan a múltiples actores del sistema.

Son las clases cuyo estado cambia y debe ser comunicado a otros componentes.  
Según el modelo final del proyecto:

- **Proyecto**
- **Etapa**
- **Tarea**

**Responsabilidades clave:**
- Mantener una lista de Observers registrados.  
- Ejecutar `notificar()` ante un cambio significativo (avance, retraso, cierre, reasignación, etc.).  
- No conocer detalles de implementación de los observadores (cumple DIP).

#### Observers existentes:
- **ServicioNotificaciones**: envía mails/WhatsApp por cambios de estado.  
- **ServicioAuditoria**: registra eventos relevantes.  
- **ResponsableDelProyecto**: actualiza su vista y pendientes.  
- **Coordinador**: recibe alertas para seguimiento estratégico.  
- **DashboardAdministrador**: actualiza tarjetas y métricas en tiempo real.

#### Observers potenciales:
- **ServicioCliente**
- **Módulo de Métricas**
- **Calendario de Recursos**

Cada observer implementa `actualizar()` y define su propia reacción.

---

## Estructura de Clases

El siguiente diagrama muestra la estructura aplicada del patrón Observer utilizando las clases reales del proyecto, basadas en:

- diagrama-clases-final.puml  
- mejoras CRC  
- matrices CLAE  
- sesión JAD  

Incluye Subjects, Observers y la interfaz común.

### Diagrama UML

![diagrama Observer](/diagramas/01-diagrama-clases/01-patron-comportamiento-observer.png)

[➡ Ver diagrama completo en detalle](/diagramas/01-diagrama-clases/01-patron-comportamiento-observer.puml)

# Justificación Técnica de la Estructura de Clases

La idea detrás de esta estructura es aplicar el patrón Observer para que las partes centrales del sistema —Proyecto, Etapa y Tarea— no tengan que preocuparse directamente por quién necesita enterarse de sus cambios.

En lugar de que cada clase sepa a quién avisar, se establece un mecanismo común: cuando algo cambia en un proyecto, una etapa o una tarea, el sistema notifica automáticamente a los módulos interesados (como responsables, coordinadores o servicios de notificación).

---

## Clases incluidas en el diagrama

### 1. `Subject` (Interfaz – Sujeto observado)
- **Responsabilidad:** Es el “contrato” que firman todos los elementos que pueden ser vigilados.  
- **Comportamiento:** Define cómo agregar un observador, cómo quitarlo y cómo avisarles cuando algo cambia.  
- **Indispensable porque:** Unifica el mecanismo de suscripción y evita duplicaciones.

---

### 2. `Observer` (Interfaz – Observador)
- **Responsabilidad:** Representa a cualquier componente que necesita enterarse de lo que pasa en el sistema.  
- **Comportamiento:** Implementa el método `actualizar(subject)`.  
- **Indispensable porque:** Desacopla la reacción de los eventos, permitiendo agregar nuevos observadores sin modificar los Subjects.

---

### `Proyecto` (Sujeto concreto)
- **Responsabilidad:** Es el nivel más alto del flujo audiovisual.  
- **Comportamiento:**  
  - Mantiene una lista de `Observer`.  
  - Invoca `notificar()` cuando su estado cambia (nueva etapa, retraso, avance global).  
- **Indispensable porque:** Es un punto crítico del flujo operativo; múltiples áreas dependen de su estado.

---

### 4. `Etapa` (Sujeto concreto)
- **Responsabilidad:** Gestiona las fases del proyecto (guion, rodaje, postproducción, etc.).  
- **Comportamiento:** Notifica cambios como atrasos, finalización o reasignación.  
- **Indispensable porque:** Los cambios en una etapa afectan al cronograma, métricas y roles responsables.

---

### 5. `Tarea` (Sujeto concreto)
- **Responsabilidad:** Representa unidades de trabajo más específicas dentro de una etapa.  
- **Comportamiento:** Notifica cuando cambia su estado (pendiente, en progreso, finalizada).  
- **Indispensable porque:** Es la unidad que más frecuentemente genera eventos dentro del flujo productivo.

---

### Observers Concretos

Los siguientes componentes implementan `Observer` y reaccionan a los cambios de cualquiera de los Subjects:

#### 6. `ServicioNotificaciones`
**Responsabilidad:** Enviar correos/WhatsApp ante cambios relevantes.  
**Indispensable porque:** Permite interacciones externas automáticas sin acoplar Subjects a infraestructura.

#### 7. `ResponsableDelProyecto`
**Responsabilidad:** Mantener su vista actualizada ante cambios significativos.  
**Indispensable porque:** Brinda seguimiento operativo en tiempo real.

#### 8. `Coordinador`
**Responsabilidad:** Recibir alertas para gestión estratégica del avance.  
**Indispensable porque:** Permite intervenciones rápidas ante desvíos.

#### 9. `DashboardAdministrador`
**Responsabilidad:** Actualizar métricas y vistas administrativas sin intervención manual.  
**Indispensable porque:** Facilita decisiones basadas en datos en tiempo real.

---

# Explicación del flujo del comportamiento (Patrón Observer)

1. Un `Subject` modifica su estado interno (un Proyecto avanza, una Etapa finaliza, una Tarea se retrasa).  
2. Llama a `notificar()`, definido en la interfaz `Subject`.  
3. `notificar()` itera sobre su lista interna de `Observer`.  
4. A cada observador se le invoca `actualizar(subject)`.  
5. Cada `Observer` interpreta el evento desde su propia lógica:  
   - El Servicio de Notificaciones envía alertas.  
   - El Responsable del Proyecto actualiza su panel.  
   - El Coordinador revisa riesgos.  
   - El Dashboard se refresca con nuevas métricas.  
6. El Subject no conoce qué hace cada Observer ni tiene dependencias directas hacia ellos.

Esto permite incorporar nuevos módulos observadores sin alterar `Proyecto`, `Etapa` o `Tarea`.

---

# Explicación técnica del patrón aplicado

En la solución se aplicó el patrón **Observer**, definiendo la interfaz `Subject` como el contrato común que expone las operaciones de suscripción (`agregarObserver`, `quitarObserver`) y de notificación (`notificar`). Las clases `Proyecto`, `Etapa` y `Tarea` interactúan únicamente con esa abstracción y delegan la gestión de los observadores mediante operaciones de alto nivel, sin conocer las implementaciones concretas.

Las implementaciones que actúan como observadores —por ejemplo `ServicioNotificaciones`, que envía correos o mensajes ante cambios relevantes— realizan directamente las acciones requeridas;  
Otros observadores como `ResponsableDelProyecto`, `Coordinador` y `DashboardAdministrador` reaccionan cada uno según su rol, actualizando vistas, recibiendo alertas o refrescando métricas, pero todos comparten el mismo punto de entrada definido por la interfaz `Observer` (`actualizar(subject)`).

Con esta organización la responsabilidad de emitir eventos queda localizada en los Subjects (`Proyecto`, `Etapa`, `Tarea`), mientras que la lógica de reacción se distribuye en los Observers. Así se elimina la duplicación de mecanismos de notificación, se reduce el acoplamiento entre capas y se facilita añadir nuevos interesados (métricas, auditoría, clientes, etc.) sin modificar las clases del dominio.  

La estructura resultante es flexible, extensible y coherente con los principios SOLID, además de alinearse con los requerimientos identificados en la sesión JAD y con las necesidades evolutivas del sistema Productora de Videos.

---
