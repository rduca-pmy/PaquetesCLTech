# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `MovimientoPublicacion`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.MovimientoPublicacion` se llena principalmente desde `510_MovimientoPublicacion.dtsx`, y tambien aparece en variantes fuera de `dtproj` orientadas a historico, ventana de 7 dias y testing. La evidencia principal observable es `OpenRowset` al destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `510_MovimientoPublicacion.dtsx` | carga principal | recurrente | paquete activo |
| `510_MovimientoPublicacionHistorico.dtsx` | variante historica | indeterminada | fuera de `dtproj` |
| `510_MovimientoPublicacion_7Dias.dtsx` | variante acotada | indeterminada | fuera de `dtproj` |
| `MovimientoPublicacionUpdateTesting.dtsx` | testing | indeterminada | fuera de `dtproj` |

## Mecanismo tecnico

- Tipo de carga: `openrowset` explicitamente observado
- Tarea o data flow: flujos de movimiento y sus variantes
- Stored procedure: no observado en la evidencia principal
- SQL relevante: destino explicito `[Activos].[MovimientoPublicacion]`
- Tabla relacionada: `Activos.MovimientoPublicacionExtension`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `510_MovimientoPublicacion.dtsx` | componente destino | `OpenRowset` apunta a `[Activos].[MovimientoPublicacion]` |
| tabla destino | `510_MovimientoPublicacionHistorico.dtsx` | componente destino | `OpenRowset` apunta a `[Activos].[MovimientoPublicacion]` |
| tabla destino | `510_MovimientoPublicacion_7Dias.dtsx` | componente destino | `OpenRowset` apunta a `[Activos].[MovimientoPublicacion]` |
| tabla destino | `MovimientoPublicacionUpdateTesting.dtsx` | componente destino | `OpenRowset` apunta a `[Activos].[MovimientoPublicacion]` |

## Hechos observados

- El paquete activo principal es `510_MovimientoPublicacion.dtsx`.
- Existen variantes fuera de proyecto que sugieren necesidades operativas o historicas.

## Inferencias

- La tabla probablemente concentra movimientos publicados en distintas ventanas o modalidades.

## Dudas abiertas

- Como se diferencian funcionalmente la version principal, historica y de 7 dias.

## Clasificacion final

- Motivo de clasificacion: destino explicito repetido en paquete principal y variantes.
- Riesgo de error: bajo sobre la existencia de sincronizacion; medio sobre el rol exacto de cada variante.
- Proxima validacion sugerida: comparar los filtros de cada variante.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `510_MovimientoPublicacion*.dtsx`
- Fecha de analisis: `2026-08-10`
