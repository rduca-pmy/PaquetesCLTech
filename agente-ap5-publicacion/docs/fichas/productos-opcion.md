# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Opcion`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.Opcion` se llena mediante `040_Productos.dtsx`. La evidencia observada combina `UPDATE` y `OpenRowset` sobre el destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete troncal de productos |

## Mecanismo tecnico

- Tipo de carga: `update + openrowset`
- Tarea o data flow: carga general de derivados
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `UPDATE [Productos].[Opcion]`
- Tablas relacionadas: `Productos.Subyacente`, `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| update | `040_Productos.dtsx` | comando SQL | aparece `UPDATE [Productos].[Opcion]` |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla se mantiene dentro del mismo job maestro.
- Comparte patron con otros derivados del esquema.

## Inferencias

- Se publica como subtipo de contrato con informacion especifica para opciones.

## Dudas abiertas

- Si existe carga adicional de valuacion o griegas por otro circuito no cubierto aqui.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita con update visible.
- Riesgo de error: bajo.
- Proxima validacion sugerida: contrastar con `Valuacion` y `Subyacente`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
