# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ListaContrato`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.ListaContrato` se llena desde varias variantes del paquete `SecurityList`, incluyendo `_100_SecurityList.dtsx`, `100_SecurityList.dtsx`, `100_SecurityListEXT.dtsx`, `100_SecurityList_FirstInsert.dtsx` y `100_SecurityList (2).dtsx`. La evidencia principal es `OpenRowset` repetido al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `_100_SecurityList.dtsx` | carga de lista | recurrente | paquete activo |
| `100_SecurityList.dtsx` | carga de lista | recurrente | paquete activo |
| `100_SecurityListEXT.dtsx` | variante EXT | recurrente | paquete activo |
| `100_SecurityList_FirstInsert.dtsx` | primera insercion | puntual o inicial | paquete activo |
| `100_SecurityList (2).dtsx` | variante duplicada | indeterminada | paquete activo |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: variantes de `SecurityList`
- Stored procedure: no observado en la evidencia principal
- SQL relevante: destino explicito `[Productos].[ListaContrato]`
- Tabla relacionada: `Productos.ListaContratoCombinado`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `_100_SecurityList.dtsx` | componente destino | `OpenRowset` apunta a `[Productos].[ListaContrato]` |
| tabla destino | `100_SecurityList.dtsx` | componente destino | `OpenRowset` apunta a `[Productos].[ListaContrato]` |
| tabla destino | `100_SecurityListEXT.dtsx` | componente destino | `OpenRowset` apunta a `[Productos].[ListaContrato]` |
| tabla destino | `100_SecurityList_FirstInsert.dtsx` | componente destino | `OpenRowset` apunta a `[Productos].[ListaContrato]` |
| tabla destino | `100_SecurityList (2).dtsx` | componente destino | `OpenRowset` apunta a `[Productos].[ListaContrato]` |

## Hechos observados

- La tabla destino aparece en multiples variantes activas.
- La familia `SecurityList` es la referencia principal para esta entidad.

## Inferencias

- La coexistencia de varias variantes sugiere distintos momentos de carga, fuentes o estrategias de inicializacion.

## Dudas abiertas

- Cual de las variantes sigue siendo la principal en produccion.
- Como se coordinan `ListaContrato` y `ListaContratoCombinado`.

## Clasificacion final

- Motivo de clasificacion: destino explicito y repetido en varias variantes activas.
- Riesgo de error: bajo sobre la existencia de sincronizacion; medio sobre el rol exacto de cada variante.
- Proxima validacion sugerida: comparar diferencias funcionales entre las variantes `SecurityList`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: familia `100_SecurityList*.dtsx`
- Fecha de analisis: `2026-08-10`
