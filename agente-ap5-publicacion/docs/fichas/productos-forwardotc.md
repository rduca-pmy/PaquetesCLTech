# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ForwardOTC`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.ForwardOTC` se llena mediante `040_Productos.dtsx`. La evidencia incluye `DELETE`, `UPDATE` y `OpenRowset`, indicando una carga con recomposicion y mantenimiento.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete troncal del esquema |

## Mecanismo tecnico

- Tipo de carga: `delete + update + openrowset`
- Tarea o data flow: carga general de productos OTC
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `DELETE [Productos].[ForwardOTC]`, `UPDATE [Productos].[ForwardOTC]`
- Tablas relacionadas: `Productos.Forward`, `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `040_Productos.dtsx` | comando SQL | aparece `DELETE [Productos].[ForwardOTC]` |
| update | `040_Productos.dtsx` | comando SQL | aparece `UPDATE [Productos].[ForwardOTC]` |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla usa el patron mas completo de mantenimiento dentro del paquete maestro.
- No se detectaron paquetes alternativos.

## Inferencias

- Es un subtipo OTC con logica propia de recarga o depuracion.

## Dudas abiertas

- Si el `DELETE` es total o segmentado por instrumento vigente.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita con mantenimiento completo.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar el criterio de borrado.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
