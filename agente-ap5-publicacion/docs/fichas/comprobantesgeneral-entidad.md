# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Entidad`
- Esquema destino: `ComprobantesGeneral`
- Clasificacion: `sincronizada`
- Dominio funcional: `ComprobantesGeneral`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `ComprobantesGeneral.Entidad` se llena mediante `Comprobantes_Entidad.dtsx`. La evidencia observable muestra `OpenRowset` directo al destino y un flujo `INSERT & UPDATE` sobre la misma tabla.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `Comprobantes_Entidad.dtsx` | carga principal | recurrente | paquete activo |

## Mecanismo tecnico

- Tipo de carga: `insert/update`
- Tarea o data flow: `INSERT & UPDATE`
- Stored procedure: no observado en la evidencia principal
- SQL relevante: lectura previa `select * from [ComprobantesGeneral].[Entidad]`
- Tabla destino: `[ComprobantesGeneral].[Entidad]`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `Comprobantes_Entidad.dtsx` | primer componente destino | `OpenRowset` apunta a `[ComprobantesGeneral].[Entidad]` |
| tabla destino | `Comprobantes_Entidad.dtsx` | `INSERT & UPDATE` | `OpenRowset` apunta a `[ComprobantesGeneral].[Entidad]` |

## Hechos observados

- El paquete figura activo en `Publicacion.dtproj`.
- La tabla destino aparece explicitamente en mas de un componente.

## Inferencias

- La tabla probablemente actua como maestro o catalogo de entidades usadas por comprobantes.

## Dudas abiertas

- Si la carga es total o incremental.

## Clasificacion final

- Motivo de clasificacion: destino explicito en paquete especifico.
- Riesgo de error: bajo.
- Proxima validacion sugerida: reconstruir la consulta origen de Clearing.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `Comprobantes_Entidad.dtsx`
- Fecha de analisis: `2026-08-11`
