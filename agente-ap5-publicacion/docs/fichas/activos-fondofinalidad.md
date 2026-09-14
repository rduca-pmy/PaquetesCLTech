# Ficha de sincronizacion AP5

## Identificacion

- Tabla destino: `FondoFinalidad`
- Esquema destino: `Activos`
- Clasificacion: `sincronizada`
- Dominio funcional: `Activos / Fondos`
- Nivel de confianza: `alta`

## Respuesta corta

La tabla `Activos.FondoFinalidad` se llena mediante `202_FondoFinalidad.dtsx`. La evidencia combina `UPDATE` y `OpenRowset`, señal de una publicacion con mantenimiento adicional sobre la tabla destino.

## Paquetes involucrados

| Paquete | Rol observado | Frecuencia inferida | Observaciones |
| --- | --- | --- | --- |
| `202_FondoFinalidad.dtsx` | carga principal | recurrente | paquete especifico para relacion fondo/finalidad |

## Mecanismo tecnico

- Tipo de carga: `update + openrowset`
- Tarea o data flow: carga de finalidad por fondo
- Stored procedure: no observada en la evidencia principal
- SQL relevante: `UPDATE [Activos].[FondoFinalidad]`
- Tablas relacionadas: `Activos.FondoCuentaDepositaria`, `Parametros.Finalidad`

## Evidencias

| Tipo | Paquete | Tarea / componente | Detalle |
| --- | --- | --- | --- |
| update | `202_FondoFinalidad.dtsx` | comando SQL | aparece `UPDATE [Activos].[FondoFinalidad]` |
| tabla destino | `202_FondoFinalidad.dtsx` | componente destino | `OpenRowset` apunta a la tabla |

## Hechos observados

- La relacion paquete-tabla es directa.
- El patron tecnico replica el usado en otras tablas de finalidad del dominio.

## Inferencias

- AP5 publica finalidades asociadas a fondos en un circuito propio del esquema `Activos`.

## Dudas abiertas

- Si el concepto de fondo aqui corresponde a FCI u otro subtipo del modelo.

## Clasificacion final

- Motivo de clasificacion: destino explicito con update visible.
- Riesgo de error: bajo.
- Proxima validacion sugerida: identificar origen exacto en `Clearing.sql`.

## Trazabilidad

- Ruta analizada: `IntegrationServices/Publicacion`
- Artefacto principal: `202_FondoFinalidad.dtsx`
- Fecha de analisis: `2026-08-11`
