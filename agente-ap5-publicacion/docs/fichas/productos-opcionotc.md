# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `OpcionOTC`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.OpcionOTC` se llena mediante `040_Productos.dtsx`. La evidencia combina `UPDATE` y `OpenRowset`, lo que sugiere insercion y mantenimiento dentro del mismo flujo.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete troncal del esquema |

## Mecanismo tecnico

- Tipo de carga: `update + openrowset`
- Tarea o data flow: carga general de productos OTC
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `UPDATE [Productos].[OpcionOTC]`
- Tablas relacionadas: `Productos.Contrato`, `Productos.Subyacente`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| update | `040_Productos.dtsx` | comando SQL | aparece `UPDATE [Productos].[OpcionOTC]` |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- El subtipo OTC vive dentro del paquete maestro de productos.
- Comparte patron con otros instrumentos derivados.

## Inferencias

- AP5 publica contratos OTC diferenciados del circuito de opcion estandar.

## Dudas abiertas

- Si existe relacion funcional estrecha con `ForwardOTC`.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita con update visible.
- Riesgo de error: bajo.
- Proxima validacion sugerida: revisar llaves y campos de valuacion del subtipo.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
