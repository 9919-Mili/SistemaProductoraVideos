# Matriz CLAE (CRUD) – Consultar Estadísticas

**Proyecto:** Sistema Productora de Videos  
**Caso de Uso:** CU5 – Consultar Estadísticas  

---

## 1) Tabla CLAE

> **Estructura:**  
> - **Filas:** Actividades internas del caso de uso (acciones o pasos del flujo).  
> - **Columnas:** Clases del sistema involucradas.  
> - **Celdas:** Letras **C**, **L**, **A**, **E** según la operación que se realiza sobre la clase.  
> - Si no aplica, dejar la celda vacía.  

| Actividad del Caso de Uso | Proyecto | Estadística | Usuario | Reporte | FiltroBusqueda |
|--------------------|:--------:|:-----------:|:-------:|:--------:|:---------------:|
| Acceder al sistema |   |   | L |   |   |
| Seleccionar módulo “Estadísticas” |   |   | L |   |   |
| Definir filtros (tipo, fecha, duración) | L |   | A |   | C |
| Solicitar consulta | L | C |   |   | L |
| Visualizar resultados | L | L | L | C |   |
| Descargar reporte | L | L |   | C |   |

> **Leyenda:**  
> **C**: Crear – **L**: Leer/Listar – **A**: Actualizar – **E**: Eliminar  

---

## 2) Métodos identificados

> Los métodos se derivan directamente de las operaciones (C/L/A/E) marcadas en la tabla.  
> Cada método deberá existir en la clase correspondiente del **diagrama de clases**, y reflejarse en su **Tarjeta CRC** y en el **diagrama de secuencia** del caso de uso.

| Clase | Método | Tipo (C/L/A/E) | Parámetros (nombre: tipo) | Retorno | Actividad asociada |
|--------|---------|----------------|----------------------------|----------|--------------------|
| FiltroBusqueda | `crearFiltro(tipoProyecto: string, fechaInicio: date, fechaFin: date)` | C | `tipoProyecto: string`, `fechaInicio: date`, `fechaFin: date` | `FiltroBusqueda` | Definir filtros |
| Estadística | `generarEstadisticas(filtro: FiltroBusqueda)` | C | `filtro: FiltroBusqueda` | `List<Estadistica>` | Solicitar consulta |
| Estadística | `listarEstadisticas()` | L | — | `List<Estadistica>` | Visualizar resultados |
| Reporte | `generarReporte(estadisticas: List<Estadistica>)` | C | `estadisticas: List<Estadistica>` | `Reporte` | Descargar reporte |
| Proyecto | `obtenerDuracionProyecto(id: int)` | L | `id: int` | `int` | Definir filtros / duración promedio |
| Usuario | `autenticarUsuario(email: string, password: string)` | L | `email: string`, `password: string` | `Usuario` | Acceder al sistema |

---

## 3) Relación con otros artefactos del diseño

| Elemento | Artefacto vinculado | Archivo / Referencia URL | Descripción de la relación |
|-----------|--------------------|-----------------------|-----------------------------|
| `generarEstadisticas()` | Diagrama de Actividad – CU5 | [`diagramas/04-diagramas-actividades/04-actividad-consultar-estadisticas.puml`]() | Representa el proceso principal de cálculo de datos. |
| `generarReporte()` | Tarjeta CRC – Reporte | [`herramientas-agile/tarjetas-crc/crc-reporte.md`]() | Figura como responsabilidad principal de la clase Reporte. |
| `crearFiltro()` | Diagrama de Secuencia – CU5 | [`diagramas/05-diagramas-secuencia/05-secuencia-consultar-estadisticas.puml`]() | Acción de inicialización de filtros antes de procesar estadísticas. |
| `obtenerDuracionProyecto()` | Diagrama de Clases | [`diagramas/03-diagramas-clases/03-diagrama-clases-general.puml`]() | Aporta datos usados en las estadísticas. |

---

## 4) Issues e inconsistencias detectadas

| URL | Descripción de la inconsistencia | Artefacto relacionado | Acción correctiva | Estado |
|----|----------------------------------|------------------------|-------------------|:------:|


**Estados posibles:** Abierto / Pendiente / Resuelto
