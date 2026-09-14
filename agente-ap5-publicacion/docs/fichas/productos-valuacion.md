# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Valuacion`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / Valuacion`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.Valuacion` se llena mediante `040_Productos.dtsx`. La evidencia muestra `DELETE` y `OpenRowset`, por lo que el paquete parece regenerar la tabla publicada.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete troncal del esquema |

## Mecanismo tecnico

- Tipo de carga: `delete + openrowset`
- Tarea o data flow: carga de valuaciones
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `DELETE [Productos].[Valuacion]`
- Tablas relacionadas: `Productos.Opcion`, `Productos.Forward`, `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| delete previo | `040_Productos.dtsx` | comando SQL | aparece `DELETE [Productos].[Valuacion]` |
| tabla destino | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La tabla se maneja dentro del paquete maestro y no en uno especifico de market data.
- El patron tecnico sugiere recarga o regeneracion.

## Inferencias

- AP5 publica valuaciones ligadas al universo de productos desde el mismo proceso maestro.

## Dudas abiertas

- Si las valuaciones son datos estaticos de configuracion o resultados actualizados periodicamente.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita con borrado previo.
- Riesgo de error: bajo.
- Proxima validacion sugerida: rastrear origen funcional en `Clearing`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
