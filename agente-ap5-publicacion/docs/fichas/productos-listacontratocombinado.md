# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `ListaContratoCombinado`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos / SecurityList`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.ListaContratoCombinado` se llena mediante el conjunto `100_SecurityList*.dtsx` y `_100_SecurityList.dtsx`. La evidencia es un `OpenRowset` directo al destino en varias variantes del mismo circuito.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `100_SecurityList.dtsx` | carga principal | recurrente | variante nominal del circuito |
| `100_SecurityList (2).dtsx` | variante activa | recurrente | version paralela observada en carpeta |
| `100_SecurityList_FirstInsert.dtsx` | carga inicial | eventual | sugiere primera poblacion |
| `_100_SecurityList.dtsx` | variante auxiliar | recurrente | paquete con prefijo especial |

## Mecanismo tecnico

- Tipo de carga: `openrowset`
- Tarea o data flow: carga de lista de contratos combinados
- Stored procedure: no observada en la evidencia principal
- SQL relevante: destino `OpenRowset` a `[Productos].[ListaContratoCombinado]`
- Tablas relacionadas: `Productos.ListaContrato`, `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `100_SecurityList*.dtsx` | componente destino | reaparece `OpenRowset` a la tabla en varias variantes |

## Hechos observados

- El circuito tiene varias versiones del mismo paquete.
- La tabla se carga desde el mismo grupo funcional que `ListaContrato`.

## Inferencias

- Se publica una lista especializada para contratos combinados o spreads.

## Dudas abiertas

- Cual de las variantes es la vigente en despliegue.

## Clasificacion final

- Motivo de clasificacion: evidencia explicita repetida en el circuito `SecurityList`.
- Riesgo de error: bajo en la relacion tecnica, medio en la vigencia exacta de variante.
- Proxima validacion sugerida: confirmar el paquete activo en el `dtproj` y el uso de `FirstInsert`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `100_SecurityList.dtsx`
- Fecha de analisis: `2026-08-11`
