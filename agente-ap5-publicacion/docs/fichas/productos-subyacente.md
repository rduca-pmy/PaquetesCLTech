# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Subyacente`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `media`

## Respuesta corta

La tabla `Productos.Subyacente` muestra evidencia en `040_Productos.dtsx` y tambien en los paquetes `Productos_FondoComunInversion*.dtsx`. La presencia de `OpenRowset` en varios jobs indica una tabla compartida por distintos circuitos de productos.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga base probable | recurrente | paquete troncal del esquema |
| `Productos_FondoComunInversion.dtsx` | actualizacion complementaria | recurrente | circuito FCI |
| `Productos_FondoComunInversionPublicacion.dtsx` | actualizacion complementaria | recurrente | circuito FCI publicado |
| `Productos_FondoComunInversionPublicacionTipoPersona.dtsx` | variante complementaria | recurrente | archivo fuera de `dtproj` |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de subyacentes desde distintos subdominios
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[Subyacente]`
- Tablas relacionadas: `Productos.Contrato`, `Productos.FondoComunInversion*`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |
| tabla destino | `Productos_FondoComunInversion*.dtsx` | componente destino | la tabla reaparece en los flujos FCI |

## Hechos observados

- No depende de un solo paquete.
- Es una tabla transversal al modelo de productos.

## Inferencias

- `Subyacente` funciona como maestro compartido por distintos tipos de instrumento.

## Dudas abiertas

- Que paquete domina la version final del dato cuando hay solapamiento.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita en varios paquetes.
- Riesgo de error: medio.
- Proxima validacion sugerida: comparar columnas y claves cargadas por cada job.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
