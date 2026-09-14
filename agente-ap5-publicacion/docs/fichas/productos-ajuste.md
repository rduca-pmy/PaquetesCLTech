# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `Ajuste`
- Esquema destino: `Productos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Productos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Productos.Ajuste` se llena principalmente desde `040_Productos.dtsx` y recibe tratamiento complementario desde variantes `Horus_Productos_Ajuste*.dtsx`. La evidencia combina `DELETE`, `UPDATE` y `OpenRowset`.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `040_Productos.dtsx` | carga principal | recurrente | paquete troncal del esquema |
| `Horus_Productos_Ajuste.dtsx` | actualizacion complementaria | recurrente | variante Horus |
| `Horus_Productos_Ajuste (1).dtsx` | variante fuera de `dtproj` | eventual | duplicado o alternativa |
| `Horus_Productos_Ajuste_.dtsx` | variante fuera de `dtproj` | eventual | duplicado o alternativa |

## Mecanismo tecnico

- Tipo de carga: `delete + update + openrowset`
- Tarea o data flow: carga general de productos y ajuste Horus
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `DELETE [Productos].[Ajuste]`, `UPDATE [Productos].[Ajuste]`
- Tablas relacionadas: `Productos.Contrato`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| carga principal | `040_Productos.dtsx` | componente destino | `OpenRowset` apunta a `[Productos].[Ajuste]` |
| mantenimiento | `Horus_Productos_Ajuste*.dtsx` | comando SQL / destino | reaparecen `DELETE`, `UPDATE` y `OpenRowset` |

## Hechos observados

- La tabla se toca desde el paquete troncal y desde el circuito Horus.
- Existen variantes fuera de `dtproj` que conviene tratar con cautela.

## Inferencias

- `Ajuste` es una entidad de producto que requiere sincronizacion adicional para el flujo Horus.

## Dudas abiertas

- Cual de las variantes Horus es la vigente.

## Clasificacion final

- Motivo de clasificacion: destino explicito en multiples paquetes.
- Riesgo de error: bajo en la relacion tecnica, medio en la vigencia exacta de variantes.
- Proxima validacion sugerida: confirmar el paquete Horus activo.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `040_Productos.dtsx`
- Fecha de analisis: `2026-08-11`
