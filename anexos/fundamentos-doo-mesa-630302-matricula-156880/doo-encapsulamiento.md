# Encapsulamiento

El encapsulamiento en este proyecto se aplica como un mecanismo de control del estado interno de las entidades principales del sistema. No se trata únicamente de ocultar atributos, sino de garantizar que cualquier modificación del modelo pase por reglas definidas por la propia clase.

En el **Sistema Productora de Videos**, las clases centrales administran información sensible como fechas, responsables, estados y credenciales. Permitir el acceso directo a estos datos generaría inconsistencias, pérdida de control y alto acoplamiento entre clases.

El diseño implementado evita estos problemas restringiendo el acceso directo a los atributos y obligando a interactuar mediante métodos públicos que contienen lógica interna y validaciones.

---

## Aplicación en el Modelo

En lugar de permitir que otras clases modifiquen listas o estados directamente, cada entidad controla su propio ciclo de vida y protege su información interna.

### Proyecto como controlador de su estado

La clase `Proyecto` administra:

- Fechas  
- Responsable general  
- Etapas  
- Clientes  

Ninguno de estos elementos puede alterarse directamente desde el exterior.

Por ejemplo:

- Las fechas se registran mediante `registrarFechas()`, lo que permite validar coherencia entre inicio y fin.  
- El responsable se modifica mediante `asignarResponsable()`.  
- Las etapas se gestionan a través de métodos específicos y no manipulando la lista directamente.  

Si los atributos fueran públicos, cualquier clase podría cambiar fechas sin validación, eliminar etapas arbitrariamente o asignar responsables inconsistentes.  
El encapsulamiento evita estos escenarios y garantiza la integridad del modelo.

---

### Etapa y control del comportamiento

La clase `Etapa` encapsula:

- Su estado  
- Sus observaciones  
- Sus adjuntos  
- Su responsable  

El cambio de estado no se realiza modificando una variable directamente, sino mediante el método `actualizarEstado()`.

Esto permite:

- Validar transiciones de estado.  
- Mantener coherencia con el proyecto.  
- Disparar notificaciones en caso de utilizar el patrón Observer.  

Aquí el encapsulamiento no solo protege datos, sino que también controla el comportamiento y las reglas de negocio asociadas.

---

### Usuario y protección de información sensible

En la clase `Usuario`, atributos como `credenciales` están completamente protegidos.

La autenticación se realiza mediante el método `autenticar()`, evitando exponer la contraseña o permitir su manipulación externa.

Además:

- Las notificaciones se agregan mediante `recibirNotificacion()`.  
- Los proyectos asignados se consultan con `consultarProyectosAsignados()`.  

Esto mejora la seguridad del sistema y reduce el acoplamiento entre componentes.

---

## Impacto en el Diseño

El encapsulamiento aplicado en el sistema permite:

- Mantener consistencia del modelo.  
- Reducir dependencias entre clases.  
- Facilitar el mantenimiento futuro.  
- Integrar patrones de diseño sin exponer estructuras internas.  
- Modificar la implementación interna sin afectar a las clases que utilizan estos objetos.  

En este proyecto, el encapsulamiento actúa como un mecanismo de estabilidad del sistema, garantizando que el dominio se mantenga coherente ante futuras modificaciones.

---

## Ejemplo de Código

```java
public class Etapa {

    private String estado;
    private List<Observacion> observaciones;

    public void actualizarEstado(String nuevoEstado) {
        if (validarTransicion(nuevoEstado)) {
            this.estado = nuevoEstado;
            notificarCambios();
        }
    }

    public void agregarObservacion(Observacion obs) {
        this.observaciones.add(obs);
    }

    private boolean validarTransicion(String nuevoEstado) {
        // Lógica interna de validación
        return true;
    }

    private void notificarCambios() {
        // Integración con Observer
    }
}
