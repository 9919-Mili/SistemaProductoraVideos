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

![diagrama Observer](/SistemaProductoraVideos/diagramas/01-diagrama-clases/01-patron-comportamiento-observer.png)

[➡ Ver diagrama completo en detalle](/SistemaProductoraVideos/diagramas/01-diagrama-clases/01-patron-comportamiento-observer.puml)

---
