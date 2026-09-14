# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `MovimientoPublicacionHistorico`
- Esquema destino: `Contabilidad`
- Clasificacion: `sincronizada`
- Dominio funcional: `Contabilidad`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Contabilidad.MovimientoPublicacionHistorico` se llena mediante `965_Movimientos.dtsx`. La evidencia visible combina `OpenRowset` al destino y `UPDATE` sobre la misma tabla, ademas de una tarea complementaria para calcular widgets.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `965_Movimientos.dtsx` | carga principal | recurrente | paquete activo y unico hallazgo claro del esquema |

## Mecanismo tecnico

- Tipo de carga: `openrowset + update`
- Tarea o data flow: `Insert & Update Movimientos`
- Stored procedure: no observado en la evidencia principal
- SQL relevante: `UPDATE [Contabilidad].[MovimientoPublicacionHistorico]`
- Tarea relacionada: `Execute CalcularWidgets`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| tabla destino | `965_Movimientos.dtsx` | componente destino | `OpenRowset` apunta a `[Contabilidad].[MovimientoPublicacionHistorico]` |
| update | `965_Movimientos.dtsx` | comando SQL | aparece `UPDATE [Contabilidad].[MovimientoPublicacionHistorico]` |
| tarea relacionada | `965_Movimientos.dtsx` | `Execute CalcularWidgets` | el paquete complementa la carga con calculo posterior |

## Hechos observados

- Es la evidencia mas clara del esquema `Contabilidad`.
- El paquete es activo en `dtproj`.

## Inferencias

- La tabla funciona como historico publicado de movimientos contables o equivalentes de AP5.

## Dudas abiertas

- Como se integra exactamente el calculo de widgets con la carga historica.

## Clasificacion final

- Motivo de clasificacion: destino explicito con update en paquete especifico.
- Riesgo de error: bajo.
- Proxima validacion sugerida: reconstruir la consulta origen y el rol de widgets.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `965_Movimientos.dtsx`
- Fecha de analisis: `2026-08-11`
